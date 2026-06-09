# Proposal Call and Strategy Alignment Plan

Generated: 2026-06-05 14:53 MDT

This is a planning document only. It does not revise `main.tex`.

## Sources Reviewed

- `main.tex`
- `esds_ai_innovation_call.pdf`
- `ESDS-AI-Strategy.pdf`
- `docs/proposal_text_improvement_plan.md`, for continuity with the prior call-only plan

I did not read `docs/study_phase_notes_jhrg.txt`.

## Work Log

### 2026-06-09 15:28 MDT

Prompt: "Using [proposal_call_strategy_alignment_plan.md](docs/proposal_call_strategy_alignment_plan.md), rewrite the `Deliverables` section of @main.tex. Put the rewritten text in the `proposal_call_strategy_alignment_plan.md document`. However, consult both the text in the that `proposal_call_strategy_alignment_plan.md document` under the `Deliverables` heading (line 221) and the existing text in the @main.tex document. Note that the text in `Approach` in the @main.tex document has not been updated yet."

Reasoning summary:

- I used the existing `Deliverables` section in `main.tex` as the starting point because it preserves the three technical parts of the proposal.
- I used the Deliverables plan below to add the mandatory call outputs that were missing: final report, open-source artifact or equivalent, and presentation/technology demonstration.
- I bounded the collection guidance deliverable to a representative reviewed set, because the current proposal text still risks overpromising all OPeNDAP-enabled ESDIS collections before the Approach section has been tightened.
- I did not edit `main.tex`; the rewritten section is added below as planning text for review.

### 2026-06-08 10:55 MDT

Prompt: "In the pal [proposal_call_strategy_alignment_plan.md](docs/proposal_call_strategy_alignment_plan.md) implement the plan in the section titled `Limitations and Challenges`. Do this by making a new section called `New Limitations and Challenges` so that I can see the current and new sections in the same document. You may edit main.tex."

Reasoning summary:

- I used the existing `Limitations and Challenges` plan bullets in this document as the requirements for the rewrite.
- I kept the current section intact and added a separate drafted replacement so you can compare the old and new text in one place.
- I translated the risk list into proposal-ready risk/mitigation prose, emphasizing reviewer concerns named elsewhere in the plan: validation, operational control, external dependencies, security, and path-to-operations realism.
- I also updated `main.tex` so the live proposal text now matches the new drafted section rather than leaving the rewrite only in the planning document.

### 2026-06-05 14:53 MDT

Prompt: "For the repo (ESDS_AI), please the read the text (@main.tex) and compare with the 'call' in [esds_ai_innovation_call.pdf](esds_ai_innovation_call.pdf) and the [ESDS-AI-Strategy.pdf](ESDS-AI-Strategy.pdf) . Show me a plan to improve the text in each section, but don't perform the steps. Instead, write that plan to the repo's docs directory. Then provide me with a summary of the 5 most important fixes to make."

Reasoning summary:

- I compared the proposal against the call's required template, requirements, mandatory deliverables, and 100-point evaluation rubric.
- I compared the proposal against the ESDS AI Strategy's pillars, operating principles, cross-cutting capabilities, boundaries, tactics, and leading indicators.
- The proposal concept is well aligned with the call because it enhances existing Hyrax, OPeNDAP, CMR, DAP4, and EDC workflows rather than proposing a new standalone AI system.
- The strongest strategy match is Infrastructure plus Access, with secondary support for Governance and Standards and some Operational Intelligence framing.
- The biggest scoring risks are not the core idea; they are missing explicitness: named validators, measurable success criteria, open-science artifacts, external model/tool dependencies, licensing/data-rights handling, and concrete operational transition gates.
- I found visible red template prompts still present in `main.tex`; these should be removed before final PDF submission.
- I rechecked `Figure3.png`; it exists in the repo even though it was omitted from an initial `rg --files` listing.

## Alignment Targets to Keep Visible

Use these as constraints when revising the proposal.

- The call requires alignment with at least one ESDS AI Strategy pillar and asks for a specific, substantive connection.
- The call gives the most weight to strategic alignment and operational relevance, 25 points each.
- The call asks for practical, near-term AI work and prefers enhancements to existing systems over greenfield development.
- The call requires a clear problem statement, why AI is the right approach, and what operational system, workflow, or community benefits.
- The call requires validation details: how the prototype will be validated, by whom, and with what success criteria.
- The call requires open-science availability of outputs and disclosure of external tools, models, platforms, data rights, and licensing considerations.
- Mandatory deliverables are a working prototype or integration, a brief final report, an open-source code repository or equivalent artifact, and a presentation with technology demonstration.
- The strategy's Infrastructure pillar directly supports metadata systems, AI-readiness standards, cloud-native formats, and open machine-readable interfaces.
- The strategy's Access pillar supports APIs, discovery interfaces, and making NASA data findable by humans and AI agents.
- The strategy's Governance and Standards capability supports review processes, metadata requirements, interoperability standards, provenance, transparency, and accountability.
- The strategy's Operational Intelligence capability supports collection health monitoring, anomaly detection, performance metrics, and user/access-pattern feedback.
- The strategy boundaries warn against new portals by default, domain-specific science validation, theoretical AI research, and AI outputs without provenance, transparency, and accountability.

## Highest-Priority Fixes

1. Remove all visible red template prompts and internal "check this" notes from
   `main.tex`. DONE jhrg 6/6/26
2. Add explicit validation metrics and named validators, especially for crawlability, metadata correctness, hallucination control, and retrieval success.
3. Rework the deliverables so they include every mandatory call deliverable: prototype or integration, final report, documented open-source artifact, and presentation/demo.
4. Make external dependencies and risk controls explicit: LLM/model choice, LangChain/LangGraph or alternatives, cloud/API costs, licensing, data rights, security, prompt injection, and human review.
5. Tighten the strategy alignment throughout: primary Infrastructure, secondary Access, and cross-cutting Governance and Standards/Operational Intelligence, using the strategy's language without overclaiming.

## Section-by-Section Plan

### Cover / Proposal Metadata DONE jhrg 6/8/26

Current fit:

- The required title, submitting organization, team lead, pillar list, and requested funding are present.
- Requested funding is within the call's expected range.
- The pillar field says Infrastructure and Access, which is the right primary framing.
- Eligibility and core ESDS portfolio participation are not obvious from the cover alone.

Plan:

- Keep Infrastructure and Access as the listed pillars; do not list Governance and Standards there because the call's cover field only names the four pillars.
- In nearby text or the Team section, make the PO.DAAC/ESDIS connection unmistakable so eligibility and operational relevance are clear.
- Add project duration/start timing only if it can be done without violating the template or consuming useful space.
- Check the requested-funding total against the budget table after rounding is settled.

### Overview and Background DONE jhrg 6/5/26

Current fit:

- The section already frames the project as an enhancement to existing EDC/Hyrax/OPeNDAP infrastructure.
- It connects to cloud-native growth, metadata quality, discoverability, and autonomous data access.
- The problem is credible but still broad; reviewers may want a sharper operational pain point.
- It uses "exabyte-scale" language, while the call and strategy use a more specific 180 PB to 600 PB growth frame.

Plan:

- Open with a concrete operational problem: metadata, access guidance, and optimization artifacts can drift from the scientific data, increasing failed discovery, failed subsetting, manual curation burden, and time-to-first-use.
- Use the call/strategy scale frame, unless another cited source supports stronger language.
- Add a concise "current state" thread: CMR records, Hyrax/OPeNDAP access, DAP4 metadata, DMR++ inventories, DAAC review, and what remains manual or brittle.
- State what has already been tried or considered: existing Hyrax directory behavior, the CMR virtual directory option, manual metadata review, and the URI proof-of-concept.
- Make "why AI" specific: an agent can inspect many collections, compare evidence across granules, draft guidance, and flag discrepancies, while deterministic CMR/OPeNDAP/PyDAP/Xarray/DMR++ checks keep factual claims grounded.
- Add a sentence connecting the problem to the strategy's time-to-first-use and NASA-data-in-external-AI-tools themes.

### Overview Subsection: Agentic Inferencing DONE jhrg 6/6/26

Current fit:

- This subsection provides the proposal's best evidence that the approach is plausible.
- It demonstrates evidence-based inference, refusal to invent unsupported metadata, and direct data probing.
- It is long enough that it may crowd out higher-scoring validation and operations material.
- It is based on a URI Hyrax proof-of-concept, not yet an EDC operational deployment.

Plan:

- Keep the subsection, but compress it to the minimum needed to prove feasibility.
- State clearly what was actually demonstrated at URI and what remains to be validated in EDC.
- Keep the strongest result: direct data probes caught wrong or missing semantic metadata while separating stated, inferred, and not-safely-guessable claims.
- Avoid implying that generic foundation models alone are the deliverable; frame them as interchangeable reasoning components inside a tool-grounded workflow.
- Move extra proof details to a citation or external artifact if page count becomes tight.

### Proposed Approach

Current fit:

- The three-part architecture is clear and maps well to discovery, metadata introspection, and in-band guidance.
- The section strongly fits the call's preference for enhancements to existing operational systems.
- The lead-in answers many call prompts, but visible red prompt text and "Check this" notes must be removed.
- The model/framework dependency strategy is still not explicit enough.

Plan:

- Remove visible red template prompt text and internal notes.
- Add one concise architecture sentence: model-agnostic LLM agent plus deterministic tool calls plus evidence schema plus human review before public guidance.
- Identify the planned orchestration layer only as far as it is true: LangChain, LangGraph, or a lightweight internal workflow runner. If undecided, say the implementation will remain framework-portable.
- State whether the project trains models. If it does not, replace "model training" language elsewhere with "model/API inference, tool execution, and validation."
- Make the open-source and provenance posture explicit here, not only in Deliverables.
- Keep each of the three parts tied to a strategy target: open machine-readable interfaces, AI-readable metadata/access guidance, and APIs/discovery for AI agents.

### Proposed Approach 2.1: AI-discoverable and Crawlable Service Interfaces

Current fit:

- This is a strong Infrastructure/Access fit and directly supports the strategy example of making the archive reachable from external AI tools.
- The OPeNDAP VDI versus CMR VDI issue is important but currently reads as friction more than as a managed decision.
- The outcome and validation criteria could be sharper.

Plan:

- State the target artifact: an AI-crawlable, web-friendly view of OPeNDAP-enabled ESDIS collections that generic AI tools can traverse without a custom NASA-only client.
- Reframe the OPeNDAP VDI and CMR VDI choice as a decision gate with criteria: ESDIS approval, compatibility with common AI tools, deployment cost, reuse by non-EDIS Hyrax servers, and consistency with CMR direction.
- Replace adversarial wording such as "hampered" with neutral operational language.
- Define success: target collections are discoverable, collection hierarchy is traversable, expected DAP4 endpoints are reachable, and crawl behavior is reproducible.
- Connect this part explicitly to not building a new portal; it exposes existing systems through machine-readable access.

### Proposed Approach 2.2: AI-assisted Metadata Introspection and Validation

Current fit:

- This is the strongest AI-specific section.
- The `usage.md` artifact is concrete and has a natural open-science story.
- The current text may over-scope by implying all OPeNDAP-enabled ESDIS collections will receive full metadata documents within the prototype.
- Hallucination control is mentioned but needs a more formal evidence and review workflow.

Plan:

- Scope the prototype carefully: crawl broad coverage if feasible, but generate and validate `usage.md` files for a representative set unless the team can defend "all collections."
- Define the `usage.md` schema: collection scope, provenance, source URLs/identifiers, variables, units, coordinates, fill values, valid ranges, temporal/spatial bounds, DMR++ chunk/access guidance, known quirks, evidence links, confidence, review status, and last-refresh time.
- Describe the workflow stepwise: select collections, query CMR, traverse Hyrax, inspect DAP4, sample with PyDAP/Xarray, inspect DMR++, run validators, compare evidence, flag discrepancies, route to expert review, publish approved guidance.
- State that generated documents do not automatically modify CMR; they surface discrepancies for expert review and possible downstream correction.
- Add staleness controls: artifact versioning, regeneration triggers, timestamps, and checks when upstream collection metadata or granule holdings change.
- Link this to Governance and Standards by emphasizing provenance, traceability, review state, and repeatable validation.
- Link this to Operational Intelligence by framing discrepancy detection as collection health monitoring for metadata/access readiness.

### Proposed Approach 2.3: Machine-actionable Guidance for Autonomous Data Retrieval Workflows

Current fit:

- The value proposition is clear: guidance travels with the data and improves first-attempt retrieval.
- It fits the strategy boundary against new portals by working through existing DAP4 responses.
- The section repeats some `usage.md` material from 2.2.
- The listing is persuasive but space-expensive and contains a syntax issue around the empty units string.

Plan:

- Focus this subsection on integration mechanics and operational value, not on regenerating the 2.2 workflow.
- Distinguish generated guidance from reviewed/approved guidance that is safe to expose in DAP4 responses.
- Explain backward compatibility: existing OPeNDAP/DAP4 clients should continue to work, while agent-aware clients can use the new guidance.
- Define acceptance criteria: an autonomous client can locate guidance in-band, choose the correct variables/conventions, and issue a valid chunk-aware subset request in representative workflows.
- Shorten the listing or convert it to a compact worked example if page count is tight.
- Clarify what was live-tested at URI and what is proposed for EDC.

### Limitations and Challenges - DONE jhrg 6/9/26

Current fit:

- The section is candid, which the call rewards.
- It names real risks around VDI approval, fast-changing AI tooling, CI/CD, and misleading generated documents.
- It does not yet cover all external dependency, licensing, data-rights, security, and operational-review concerns the call asks reviewers to assess.

Plan:

- Rewrite as risk plus mitigation pairs.
- Include these risks: VDI decision/approval, agent hallucination, false positives/false negatives, external model or framework changes, licensing and data-rights constraints, cloud/API cost variability, prompt injection or malicious content in agent-readable pages, stale guidance, reviewer capacity, DAAC bucket/publication ownership, and scope control.
- Pair each risk with controls: fallback interface path, deterministic validators, evidence tags, confidence labels, refusal behavior, human review, model abstraction, open-source code, CI/CD, test collections, versioning, security review, and decision gates.
- Keep the cohort-learning point, but attach it to concrete unknowns such as tool maturity and operational practices.
- Remove informal or awkward phrasing during final editing.

### New Limitations and Challenges - THIS IS AI's TAKE ON A REWRITE. NOT USED jhrg 6/8/26

This project carries both technical and operational risk, so we will manage each major risk with a specific control and fallback path. For Part 1, deployment of the Virtual Directory Interface depends in part on \ac{ESDIS}, \ac{CMR}, and \ac{DAAC} operational decisions, including approval of where the interface is hosted and who owns publication into production buckets or service endpoints. If deployment approval is delayed or denied, we will still deliver the crawlable interface as an open, documented prototype integrated with Hyrax and validated against representative collections, while documenting the remaining operational steps needed for \ac{EDC} adoption.

For Part 2, the central risk is that an agentic workflow could generate incorrect or incomplete collection guidance through hallucination, false positives, or false negatives. We will reduce that risk by constraining the agent to tool-mediated inspection of \ac{CMR}, \ac{CF}, \ac{DAP4}, and data-derived evidence; by requiring evidence tags, confidence labels, and explicit refusal behavior when the system cannot justify a claim; and by running deterministic validators and regression tests on representative collections. Reviewed guidance will be treated as an approved artifact, not as raw model output.

The project also depends on a rapidly changing external \ac{AI} software ecosystem, including models, orchestration frameworks, and cloud or \ac{API} pricing. To keep those dependencies from driving the design, we will isolate model-specific logic behind stable interfaces, keep the core software open source and testable without a single vendor dependency, track versioned prompts and tool schemas in \ac{CICD}, and use decision gates to limit scope if a framework or model path becomes unstable or cost-prohibitive.

Because the system will consume machine-readable web content and metadata, it must also account for prompt injection, malicious or malformed agent-readable pages, stale guidance, and licensing or data-rights constraints on derived artifacts. We will address those risks through source allow-lists, content validation, provenance capture, versioning of generated guidance, human review before publication, and security review before exposing any new in-band guidance through operational \ac{DAP4} responses. We will also bound the number of collections and publication targets addressed during the project so reviewer capacity and operations coordination remain realistic.

Finally, we expect some project risks to come from operational practices that are still emerging across the community, not only from the code itself. We will use the cohort-learning structure of this call to compare validation methods, security practices, and operational transition patterns with peer teams, while still relying on our own test collections, review checkpoints, and deployment criteria to decide what is mature enough to release.

### Deliverables

Current fit:

- The three deliverables mirror the three technical parts.
- The section is missing some mandatory call deliverables.
- It promises public metadata documents and tutorials, but the number/scope of collections is not bounded.

Plan:

- Reshape the list around concrete artifacts that exist at the end of the project:
  - Working AI-crawlable Hyrax/OPeNDAP interface prototype or integration.
  - Agentic metadata introspection software with documented tool calls, schemas, tests, and validation scripts.
  - Reviewed `usage.md` artifacts for a named or representative set of collections.
  - Prototype Hyrax/DAP4 exposure of reviewed guidance, or a documented integration path if deployment approval is outside project control.
  - Open-source repository or equivalent accessible artifact, with documentation.
  - Brief final report under 10 pages covering what was built, validation, lessons learned, and path to operations.
  - Presentation and technology demonstration for the Earth Data Officer and leadership team.
- Add acceptance evidence for each deliverable where possible.
- Avoid promising "all OPeNDAP-enabled data in ESDIS" unless that scope is defensible within 9 months and the budget.
- Make open-science availability explicit: code, schemas, sample artifacts, documentation, and validation results should be public unless restricted by NASA policy.

### New Deliverables - THIS IS AI's TAKE ON A REWRITE. NOT USED jhrg 6/9/26

\section{Deliverables}

We will produce the following artifacts that satisfy the required deliverables
while preserving provenance, review status, and a clear path to \ac{EDC}
operations. The deliverables are: 

\begin{enumerate} 

\item \textbf{An \ac{AI}-crawlable Hyrax/\acs{OPeNDAP} interface.} We will
deliver a working Virtual Directory Interface for representative
    \acs{OPeNDAP}-enabled \ac{ESDIS} collections, using either the existing
    \acs{OPeNDAP} Hyrax interface or the \ac{CMR} virtual directory path
    selected with \ac{ESDIS} guidance. The acceptance evidence will show that
    generic \ac{AI} tools can discover target collections, traverse the
    collection structure, and reach the expected \ac{DAP4} service endpoints
    without collection-specific adaptation. If production deployment approval is
    outside the project's control during the award period, we will deliver the
    working Hyrax prototype and a documented integration path for \ac{EDC}.

    \item \textbf{Agentic metadata introspection and validation software.} We
    will deliver open-source software that crawls selected
    \acs{OPeNDAP}-enabled collections, queries \ac{CMR}, inspects
    \acs{OPeNDAP}/\ac{DAP4} responses, samples representative granules using 
    \acs{OPeNDAP}, examines \ac{DMR++} access structure where available,
    and drafts evidence-linked collection guidance. The repository will include
    tool-call definitions, schemas, prompts or workflow configuration,
    validation scripts, regression tests, and developer documentation. The
    acceptance evidence will show that the workflow distinguishes stated facts,
    defensible inferences, uncertain claims, and unsupported claims.

    \item \textbf{Reviewed collection-level \texttt{usage.md} artifacts.} For a
    named or representative set of collections selected with \ac{ESDIS} and
    \ac{DAAC} partners, we will deliver reviewed Markdown guidance files that
    summarize collection scope, provenance, source identifiers, variables,
    units, coordinates, fill values, value ranges, temporal and spatial bounds,
    chunking and access guidance, known access issues, evidence links,
    confidence labels, review status, and last-refresh time. Generated guidance
    will not be treated as authoritative until it has passed validation and
    expert review. Public sample artifacts and validation results will be made
    available unless restricted by \ac{NASA} policy.

    \item \textbf{Prototype exposure of approved guidance through
    Hyrax/\ac{DAP4}.} We will deliver a prototype or integration path that makes
    reviewed guidance available through existing Hyrax/\ac{DAP4} responses so
    autonomous clients can use the guidance at the point of retrieval. Existing
    \acs{OPeNDAP} clients should continue to work without change, while
    agent-aware clients will be able to locate the approved guidance and use it
    to issue valid, chunk-aware subset requests in representative workflows.

    \item \textbf{Open-science repository and documentation.} We will provide a
    public GitHub repository artifact containing the
    prototype software, schemas, sample \texttt{usage.md} files, validation
    scripts, test cases, documentation, and user-facing examples. This artifact
    will document external model, framework, platform, licensing, and data-rights
    assumptions needed to reproduce or extend the work.

    \item \textbf{Final report, presentation, and technology demonstration.} At
    the end of the project, we will provide a brief final report of no more than
    ten pages describing what was built, how it was validated, what was learned,
    remaining risks, and the recommended path to operations. We will also
    provide a presentation and technology demonstration for the Earth Data
    Officer and the leadership team, showing the crawlable interface, the
    metadata-introspection workflow, reviewed guidance artifacts, and the
    retrieval workflow enabled by in-band guidance.
\end{enumerate}

### Validation and Path to Operations

Current fit:

- The current section is substantially improved compared with the old empty placeholder.
- It still needs named validators, success thresholds, and operational transition gates.
- It does not yet explicitly address open science in the way the call asks.

Plan:

- Add measurable success criteria:
  - Crawlability: number or percentage of target collections discovered and traversed.
  - Endpoint reachability: expected CMR, Hyrax, and DAP4 endpoints reached reproducibly.
  - Metadata quality: expert-confirmed precision/recall or categorized discrepancy outcomes for generated claims.
  - Hallucination control: unsupported claims are refused or labeled uncertain.
  - Retrieval success: autonomous clients complete correct subset requests more often than a baseline without embedded guidance.
  - Efficiency: fewer avoidable retries, better chunk alignment, or reduced time-to-first-use in selected workflows.
- Name validators if confirmed: Ed Armstrong/PO.DAAC for DAAC/domain review, OPeNDAP engineering for Hyrax integration, and ESDIS/DAAC partners for operational fit.
- If a validator is not confirmed, say "to be confirmed with ESDIS/DAAC partners" rather than inventing commitment.
- Define path-to-operations gates: ESDIS choice of VDI path, security/data-rights review, human review workflow for generated artifacts, CI/CD, maintenance ownership, pilot collection rollout, and criteria for expanding beyond pilot collections.
- Add open-science validation artifacts: scripts, test cases, generated sample guidance, and validation results in the public repo when policy allows.

### Timeline

Current fit:

- The 9-month schedule is within the call's 12-month maximum.
- It has clear parts and decision points.
- It lacks an absolute final date, because the start date is not stated in the proposal.

Plan:

- Keep the 9-month structure if scope is limited to representative collections and a prototype/integration path.
- If the project period is assumed to start no later than September 1, 2026, state the final deliverable month/date accordingly; otherwise avoid inventing a calendar date.
- Add or preserve decision points at Month 2, Month 6, and Month 8.
- Add a validation/output detail to each month so the schedule reads as deliverable-driven rather than activity-only.
- Consider whether 12 months would be more credible if the plan continues to imply broad ESDIS collection coverage.

### Team

Current fit:

- The table lists people, roles, and person-months.
- It includes PO.DAAC and unfunded domain collaborators, which helps validation credibility.
- It could make the core ESDS portfolio connection and role-to-work-package mapping clearer.

Plan:

- Tie each funded person to specific work packages:
  - James Gallagher: project lead, Hyrax/OPeNDAP architecture, VDI path, agent workflow, and integration.
  - Hannah Robertson: agent workflow implementation, validators, tests, schemas, documentation, and CI/CD.
  - Ed Armstrong: PO.DAAC/DAAC validation, representative collection selection, operational review, and domain feedback.
- Keep unfunded collaborators, but do not make core deliverables depend on unfunded labor unless that is intentional and defensible.
- Add external dependencies explicitly: ESDIS guidance on VDI path, DAAC reviewers, and any approval needed for EDC deployment.
- Confirm that the funded team lead and institutional authorization requirements are satisfied outside the proposal text, or make the relevant connection clearer if needed.
- Fix grammar in the budget/personnel prose where roles are summarized.

### Budget Summary

Current fit:

- The table is present and the total is in the expected call range.
- The personnel subtotal appears to differ by one dollar depending on rounding.
- The narrative has typos and likely overstates compute purpose by saying "model training" if no training is planned.
- Tooling is marked `n/a`, while the call expects tooling costs to be disclosed if present.

Plan:

- Recalculate the personnel and total costs after rounding rules are chosen; make table and narrative consistent.
- Replace "AI model training and inference" with "AI model/API inference, tool execution, validation, and cloud testing" unless actual training is planned.
- Fix typos: `LanChain` to `LangChain`, "AWS computer" to "AWS compute", and grammar in the personnel paragraph.
- If tooling cost is zero, say zero or included in compute/personnel, rather than `n/a`.
- Keep the no-hardware and no-travel statements because they align well with the call.
- Tie the compute estimate to assumptions at a high level: LLM API calls, AWS compute/storage for validation, and automated test runs.
- State licensing/data-rights assumptions for commercial models or platforms if any cost line depends on them.

### References, Acronyms, and Cross-Cutting Cleanup

Current fit:

- The proposal has citations and acronym handling, but final polish is still needed.
- Several visible red template prompts remain.
- Some comments and informal phrases are harmless in source but risky if they compile or distract during review.

Plan:

- Remove visible red call-template prompts before final PDF generation.
- Leave source comments only if they do not compile into the PDF; remove any visible internal notes.
- Check every proof-of-concept claim against `references.bib` and the cited artifact.
- Review page count early; the proposal likely needs compression to make room for validation, deliverables, and dependency language.
- Confirm that all literal Markdown artifacts render correctly in LaTeX, especially `usage.md`, backticks, listings, and quotes.
- Ensure final wording never implies AI-generated metadata becomes authoritative without human review and provenance.
