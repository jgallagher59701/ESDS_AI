# LangChain Tool Call Monthly Cost Baseline

Generated: 2026-05-29 17:08:38 MDT

## Prompt

But what would this cost? I need a baseline to estimate monthly compute costs - where I suspect that agents will have to make many more than 10K calls - lets say 1M/month and again, assume LangChain.

## Short Answer

For 1M LangChain tool calls per month, the AWS compute cost is probably small if the tools are mostly CMR/API calls. The expensive part is only if each tool call is wrapped in one or more LLM calls.

Approximate monthly baseline:

| Scenario | Monthly baseline |
|---|---:|
| CMR/API tools invoked directly by a batch worker, no LLM per call | $25-$100 |
| Same, but private subnet with NAT Gateway | $60-$150 |
| Agent-mediated calls using a small LLM every time | $200-$3,000+ |
| Heavier reasoning model, large tool outputs in prompt | $5,000-$25,000+ |

LangChain itself is mostly Python orchestration. The bill comes from AWS runtime, storage/logging, and model tokens.

## AWS-Only Baseline

Assumptions:

- 1M CMR/tool HTTP calls per month.
- Average response stored/logged: 25-50 KB.
- Fargate worker, Linux/x86, `1 vCPU / 2 GB`.
- Worker is rate limited to 5-20 requests/sec.
- S3 stores raw or normalized results.
- DynamoDB or SQS tracks status.

Using AWS Fargate US East example pricing:

```text
vCPU:   $0.000011244/sec * 3600 = about $0.0405/hour
memory: $0.000001235/sec * 2 GB * 3600 = about $0.0089/hour
total:  about $0.049/hour
```

If the worker runs only when needed:

```text
1M calls at 10 calls/sec = 100,000 seconds = 27.8 hours
27.8 hours * $0.049/hour = about $1.40
```

If one worker runs continuously all month:

```text
730 hours * $0.049/hour = about $36/month
```

This means CMR-scale harvesting is not CPU-heavy. It is mostly network I/O and rate limiting.

## Likely AWS Add-Ons

Approximate monthly costs for 1M calls:

| Item | Rough cost |
|---|---:|
| Fargate batch worker | $2-$40 |
| S3 PUTs, if 1 object per call | about $5 per 1M PUTs |
| S3 storage, 25-50 GB | about $1-$2 |
| DynamoDB status table | about $1-$5 |
| SQS queue | about $0-$2 |
| CloudWatch logs, depending verbosity | $0-$10 |
| Public IPv4 or NAT, if used carelessly | $4-$40+ |

Notes:

- If results are batched into larger JSONL or Parquet files, S3 request cost drops.
- If each call logs many KB, CloudWatch Logs can become more noticeable.
- If workers live in private subnets, NAT Gateway fixed and per-GB costs should be included.
- CMR may return `429` responses. Budget for retries and design for `retry-after`.

## LLM Cost Is the Swing Factor

If an agent uses an LLM around each tool call, model tokens dominate.

Example with 1M agent steps per month:

```text
1,500 input tokens per step
250 output tokens per step
```

Approximate monthly model costs:

| Model | Monthly token cost |
|---|---:|
| GPT-5 nano | about $175 |
| GPT-5 mini | about $875 |
| GPT-4.1 mini | about $1,000 |
| GPT-5 | about $4,375 |

If each step includes larger CMR JSON/tool output:

```text
5,000 input tokens per step
500 output tokens per step
```

Then GPT-5 mini is about:

```text
5,000 * $0.25 + 500 * $2.00 = $2,250/month
```

The simplest way to keep costs down is to have tools return compact facts and store raw JSON in S3, rather than sending large CMR responses back into the model context.

## Recommended Proposal Baseline

For proposal budgeting:

```text
AWS batch/queue/storage/logging for 1M CMR-like tool calls:
  $100/month baseline

LLM/API inference for agent-mediated extraction:
  $1,000-$3,000/month baseline

Safety factor:
  2x, because failed calls, retries, larger prompts, and validation runs add up

Practical monthly compute estimate:
  $2,500-$6,000/month
```

For a 9-12 month project, a reasonable compute budget line would be about:

```text
$25K-$50K total
```

That number assumes real agent runs at scale. If the system mostly invokes deterministic tools and uses LLMs only for summarization, review, and selected reasoning steps, the actual AWS compute cost could be closer to hundreds of dollars per year.

## Cost Control Guidance

- Separate deterministic tool execution from LLM reasoning.
- Do not pass full CMR JSON payloads into the model unless needed.
- Store raw results in S3 and pass compact summaries into the agent.
- Rate-limit CMR calls and honor `429` plus `retry-after`.
- Use Fargate or Batch for longer PyDAP/Xarray/OPeNDAP work.
- Use Lambda only for small, short tasks.
- Prefer public-subnet batch workers for cheap outbound API access unless security policy requires private subnets plus NAT.
- Track cost per run: number of tool calls, model input tokens, model output tokens, retries, bytes stored, and bytes transferred.

## Sources

- AWS Fargate pricing: https://aws.amazon.com/fargate/pricing/
- AWS S3 pricing: https://aws.amazon.com/s3/pricing/
- AWS CloudWatch pricing: https://aws.amazon.com/cloudwatch/pricing/
- AWS DynamoDB pricing: https://aws.amazon.com/dynamodb/pricing/
- AWS Lambda pricing and quotas: https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html
- CMR Search API: https://cmr.earthdata.nasa.gov/search/site/docs/search/api.html
- OpenAI API pricing: https://platform.openai.com/docs/pricing/

## Work Log

### 2026-05-29 17:08:38 MDT

Prepared this Markdown file from the prior discussion about estimating monthly compute costs for 1M LangChain tool calls. The document separates AWS infrastructure costs from model-token costs because the latter dominates if every tool call is agent-mediated.
