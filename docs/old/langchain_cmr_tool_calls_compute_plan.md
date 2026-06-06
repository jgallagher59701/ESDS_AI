# LangChain CMR Tool Calls and AWS Compute Plan

Generated: 2026-05-29 17:08:38 MDT

## Prompt

Suppose we decide to implement tools using LangChain (tools to extract information from CMR, etc.). And make 10K calls to those tools, what would the code be? What kinds of compute resources would we need (assume we have an AWS account and can make any kind of instnace it offers, along with all the other cloud infrastructure choinces). We have familiarity with Terraform.

## Short Answer

10K CMR-style tool calls is not a large AWS compute problem. It is mostly an I/O, rate-limit, retry, logging, and provenance problem.

Do not put 10K calls inside one free-running LLM agent loop. Define LangChain tools, then run those tools with a deterministic batch or queue worker. Use an agent for planning, summarizing, or deciding which tools to use for a scoped task, not for brute-force execution.

## Implementation Pattern

Use LangChain tools as typed wrappers around CMR operations, then invoke them directly from an async runner.

```python
# cmr_tools.py
import asyncio
import os
import time
import uuid
from typing import Any

import httpx
from langchain.tools import tool
from pydantic import BaseModel, Field

CMR_BASE = "https://cmr.earthdata.nasa.gov/search"
CLIENT_ID = os.getenv("CMR_CLIENT_ID", "opendap-esds-ai-prototype")
CMR_RPS = float(os.getenv("CMR_RPS", "10"))


class SimpleRateLimiter:
    def __init__(self, rps: float):
        self.min_interval = 1.0 / rps
        self._lock = asyncio.Lock()
        self._last = 0.0

    async def wait(self) -> None:
        async with self._lock:
            now = time.monotonic()
            delay = self.min_interval - (now - self._last)
            if delay > 0:
                await asyncio.sleep(delay)
            self._last = time.monotonic()


_limiter = SimpleRateLimiter(CMR_RPS)
_client: httpx.AsyncClient | None = None


async def get_client() -> httpx.AsyncClient:
    global _client
    if _client is None:
        _client = httpx.AsyncClient(timeout=30.0)
    return _client


async def cmr_get(
    path: str,
    params: dict[str, Any],
    extra_headers: dict[str, str] | None = None,
) -> dict[str, Any]:
    headers = {
        "Accept": "application/json",
        "Client-Id": CLIENT_ID,
        "X-Request-Id": str(uuid.uuid4()),
    }
    if extra_headers:
        headers.update(extra_headers)

    client = await get_client()
    url = f"{CMR_BASE}/{path}"

    for attempt in range(6):
        await _limiter.wait()
        response = await client.get(url, params=params, headers=headers)

        if response.status_code == 429:
            await asyncio.sleep(float(response.headers.get("retry-after", "1")))
            continue

        if 500 <= response.status_code < 600:
            await asyncio.sleep(min(30, 2**attempt))
            continue

        response.raise_for_status()
        return {
            "url": str(response.url),
            "cmr_hits": response.headers.get("CMR-Hits"),
            "cmr_request_id": response.headers.get("CMR-Request-Id"),
            "cmr_search_after": response.headers.get("CMR-Search-After"),
            "body": response.json(),
        }

    raise RuntimeError(f"CMR request failed after retries: {url}")


class CollectionSearchInput(BaseModel):
    provider: str | None = None
    service_type: str | None = "OPeNDAP"
    keyword: str | None = None
    page_size: int = Field(default=100, ge=1, le=2000)


@tool(args_schema=CollectionSearchInput)
async def cmr_search_collections(
    provider: str | None = None,
    service_type: str | None = "OPeNDAP",
    keyword: str | None = None,
    page_size: int = 100,
) -> dict[str, Any]:
    """Search NASA CMR collections, optionally filtering for OPeNDAP-enabled collections."""
    params: dict[str, Any] = {"page_size": page_size}

    if provider:
        params["provider"] = provider
    if service_type:
        params["service_type[]"] = service_type
    if keyword:
        params["keyword"] = keyword

    return await cmr_get("collections.json", params)


class GranuleSearchInput(BaseModel):
    collection_concept_id: str
    page_size: int = Field(default=100, ge=1, le=2000)
    cmr_search_after: str | None = None


@tool(args_schema=GranuleSearchInput)
async def cmr_search_granules(
    collection_concept_id: str,
    page_size: int = 100,
    cmr_search_after: str | None = None,
) -> dict[str, Any]:
    """Search CMR granules for one collection concept id."""
    headers = {}
    if cmr_search_after:
        headers["CMR-Search-After"] = cmr_search_after

    return await cmr_get(
        "granules.json",
        {"collection_concept_id": collection_concept_id, "page_size": page_size},
        extra_headers=headers,
    )
```

Run the tools with an async batch worker:

```python
# run_10k.py
import asyncio
import json
from pathlib import Path

from cmr_tools import cmr_search_granules

OUT = Path("results.jsonl")


async def run_one(collection_concept_id: str) -> dict:
    return await cmr_search_granules.ainvoke(
        {"collection_concept_id": collection_concept_id, "page_size": 100}
    )


async def run_many(collection_ids: list[str], concurrency: int = 25) -> None:
    sem = asyncio.Semaphore(concurrency)

    async def guarded(cid: str):
        async with sem:
            try:
                result = await run_one(cid)
                return {"ok": True, "collection_concept_id": cid, "result": result}
            except Exception as exc:
                return {"ok": False, "collection_concept_id": cid, "error": repr(exc)}

    with OUT.open("a") as f:
        for task in asyncio.as_completed([guarded(cid) for cid in collection_ids]):
            row = await task
            f.write(json.dumps(row) + "\n")
            f.flush()


if __name__ == "__main__":
    ids = Path("collection_ids.txt").read_text().splitlines()
    asyncio.run(run_many(ids[:10_000]))
```

Use an agent for scoped reasoning or summarization:

```python
from langchain.agents import create_agent
from cmr_tools import cmr_search_collections, cmr_search_granules

agent = create_agent(
    model="provider:model-name",
    tools=[cmr_search_collections, cmr_search_granules],
)

result = agent.invoke({
    "messages": [
        {
            "role": "user",
            "content": "Find OPeNDAP collections for PODAAC and summarize which metadata fields should be validated.",
        }
    ]
})
```

## AWS Compute Resources

For 10K CMR-only calls, start small:

- One AWS Batch or ECS Fargate worker.
- `0.5 vCPU / 1 GB` for simple CMR requests.
- `1 vCPU / 2 GB` if LangChain, JSON normalization, retries, and logging are all inside the worker.
- `2 vCPU / 4-8 GB` if tools perform PyDAP/Xarray/OPeNDAP sampling or parse larger metadata/data responses.

Lambda is also possible for small, short jobs, but Fargate or Batch is more flexible once the worker includes PyDAP, Xarray, NetCDF/HDF libraries, or longer-running validation workflows.

## Terraform-Managed Infrastructure

Expected resources:

- `aws_s3_bucket`: raw CMR responses, normalized records, generated `usage.md` files.
- `aws_ecr_repository`: container image for the worker.
- `aws_ecs_cluster` or AWS Batch compute environment.
- `aws_batch_job_queue` and `aws_batch_job_definition`, or ECS run task definitions.
- `aws_sqs_queue` plus DLQ if using one message per collection/tool call.
- `aws_dynamodb_table`: run status, idempotency, retries, per-collection state.
- `aws_cloudwatch_log_group`: logs, CMR request IDs, errors, metrics.
- `aws_iam_role`: task role with S3, DynamoDB, SQS, and logging permissions.
- `aws_secretsmanager_secret` or SSM Parameter Store: Earthdata/model/API tokens if needed.

Networking choices:

- CMR is a public endpoint, so workers need outbound internet access.
- Public subnet plus assigned public IP is often cheaper for batch jobs.
- Private subnet plus NAT Gateway is operationally common but adds fixed monthly cost and per-GB processing cost.
- Add S3 VPC endpoints if moving large internal data volumes.

## Rate and Runtime Estimate

Approximate wall-clock time:

```text
wall time ~= number_of_calls / allowed_requests_per_second
```

Examples:

- 10K calls at 10 requests/sec: about 17 minutes.
- 10K calls at 25 requests/sec: about 7 minutes.

The practical limit should come from CMR behavior and `429` handling, not from AWS maximum parallelism.

## Key Design Guidance

- Use LangChain tools as typed wrappers.
- Run high-volume work with deterministic workers, not one giant agent conversation.
- Have tools return compact facts and store raw JSON in S3.
- Preserve CMR request IDs for reproducibility.
- Add retries, backoff, and rate limiting from the beginning.
- Make each tool idempotent so failed jobs can be retried safely.

## Sources

- LangChain tools: https://docs.langchain.com/oss/python/langchain/tools
- LangChain agents: https://docs.langchain.com/oss/python/langchain/agents
- CMR Search API: https://cmr.earthdata.nasa.gov/search/site/docs/search/api.html
- AWS Fargate pricing: https://aws.amazon.com/fargate/pricing/
- AWS Batch on Fargate: https://docs.aws.amazon.com/batch/latest/userguide/fargate.html
- AWS Lambda quotas: https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html

## Work Log

### 2026-05-29 17:08:38 MDT

Prepared this Markdown file from the prior discussion about LangChain tools, CMR API calls, 10K tool invocations, AWS compute choices, and Terraform-managed infrastructure. The result is a planning/reference document only; it does not implement the code.
