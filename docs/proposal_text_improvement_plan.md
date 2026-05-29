# ESDS AI Proposal Text Improvement Plan

Generated: 2026-05-29 15:08:49 MDT

This is a planning document only. It does not revise `main.tex`; it lists recommended edits to make later.

## Sources Reviewed

- `AGENTS.md`
- `main.tex`
- `esds_ai_innovation_call.pdf`

I did not read `docs/study_phase_notes_jhrg.txt`.

## Work Log

### 2026-05-29 15:08:49 MDT

Prompt: "For the repo at /Users/jhrg/src/opendap/ESDS_AI, I have updated AGENTS.md. For this repo, please the text and compare with the 'call' in @esds_ai_innovation_call.pdf. Show me a plan to improve the text in each section, but don't perform the steps. Instead, write that plan to the repo's `docs` directory. For sections that are empty, you may suggest content or skip them. Timeline section, you may skip or make suggestions."

Reasoning summary:

- The call asks proposals to follow Appendix A exactly and not add or reorganize sections.
- The scoring rubric weights strategic alignment and operational relevance most heavily: 25 points each.
- The proposal already has a strong operational-system premise, because it extends Hyrax, OPeNDAP, and EDC workflows rather than proposing a greenfield AI system.
- The largest gaps are the empty validation and budget sections, the missing requested-funding field, several unsupported claims that need evidence or citations, and the need to state the AI tools/models/frameworks more concretely.
- The `opendap` conda environment mentioned in `AGENTS.md` was not available in this shell. I used the available local Python only to extract text from the PDF after `pdftotext` was not installed.

## Call Requirements to Keep Visible

- Use the template sections in Appendix A.
- Keep to the 6-page limit, excluding cover page, budget table, work effort table, and references.
- Include the requested funding amount on the cover page.
- Connect clearly to at least one ESDS AI Strategy pillar.
- Prefer enhancements to existing applications or systems over greenfield development.
- Define the problem and why AI is the right approach.
- Identify a specific operational system, workflow, or user community that benefits.
- Include a validation plan, success criteria, and who validates the output.
- State how outputs will be openly available under NASA open science policy.
- Disclose dependencies on external tools, models, platforms, data rights, and licensing.
- Address mandatory deliverables: working prototype or integration, final report, open-source repository or equivalent artifact, and presentation plus technology demonstration.

## Highest-Priority Improvements

1. Fill `Validation and Path to Operations`; this is both empty and directly scored.
2. Fill `Budget Summary` and add `Requested Funding` to the title block.
3. Rewrite the `Proposed Approach` lead-in to remove internal notes and explicitly name the AI architecture, tools, models, and validation controls.
4. Tighten `Overview and Background` around a specific ESDS operational problem and why AI is needed.
5. Rework `Deliverables` so it includes the call's mandatory final report, open-source artifact, and presentation/demo.
6. Add evidence or citations for claims marked or implied as unsupported, especially proof-of-concept claims.

## Section-by-Section Plan

### Cover / Proposal Metadata

Current fit:

- Includes title, submitting organization, team lead, and ESDS pillars.
- Missing the call's `Requested Funding` field.
- Eligibility connection to the core ESDS portfolio is implicit through PO.DAAC collaboration, but not obvious in the metadata.

Plan:

- Add `Requested Funding` once the amount is known.
- Consider shortening the title so reviewers can quickly see the core value: AI-assisted metadata curation and agent-ready OPeNDAP access.
- If appropriate, make the PO.DAAC or ESDIS connection more visible in the cover metadata or Team section so eligibility is unambiguous.
- Keep the pillar list focused. Infrastructure and Access are clearly supported; Analysis is plausible, but should be justified explicitly if retained.

### Overview and Background

Current fit:

- Strong alignment with the call's preference for enhancements to existing systems.
- Good emphasis on Hyrax, EDC, cloud-native access, metadata quality, and agent-assisted workflows.
- The problem is broad and somewhat abstract; reviewers may want a crisper operational pain point.
- Some claims need evidence, examples, or citations before final submission.

Plan:

- Open with a concrete problem statement: metadata and access guidance can drift from the underlying data, which harms discovery, subsetting, interoperability, and autonomous workflows.
- Use the call's own scale framing, such as current ESDS petabyte scale and projected growth, without overextending into unsupported exabyte language unless cited.
- Add a short "current state" thread: CMR metadata, DMR++ inventories, DAAC/EDC curation, Hyrax service behavior, and what remains manual or brittle.
- State what has already been tried or considered: existing OPeNDAP/Hyrax interfaces, CMR virtual directory work, manual metadata review, and the proof-of-concept crawl if documented.
- Make "why AI" sharper: AI is useful for scalable inspection, cross-granule comparison, anomaly detection, and generating machine-actionable guidance, while deterministic OPeNDAP/PyDAP/Xarray checks provide evidence.
- Avoid unsupported superlatives such as "nowhere else" unless backed by evidence.
- Fix prose-level issues later, including the awkward phrase "OPeNDAP and the data-proximate and subset-driven protocol."

### Proposed Approach

Current fit:

- The three-part structure is clear and maps well to discovery, metadata generation, and operational delivery.
- The approach strongly matches the call's preference for enhancing existing operational systems.
- The opening lines read like internal notes and include Markdown-style emphasis inside LaTeX text.
- The section does not yet clearly answer the call's question about which AI tools, models, or frameworks will be used and why.

Plan:

- Replace the internal explanatory lead-in with a polished roadmap paragraph that says what will be built, how the parts depend on each other, and what operational system is enhanced.
- Explicitly describe the AI architecture at a non-hand-wavy level:
  - LLM-backed agent or workflow controller.
  - Tool calls/functions for CMR discovery, OPeNDAP/DAP4 access, PyDAP/Xarray sampling, DMR++ inspection, and evidence capture.
  - Deterministic validators for units, coordinate conventions, ranges, fill values, chunk layout, and cross-granule consistency.
  - Human review before public or operational publication of generated guidance.
- Decide whether LangChain, LangGraph, or another framework is actually part of the implementation. If yes, mention it here, not only in Limitations, and explain why.
- Clarify model dependency strategy: identify whether a specific commercial model is required, whether model choice is swappable, and how licensing/data-rights issues are handled.
- Convert proof-of-concept material into concise evidence: what was demonstrated, where, what it proves, and what still needs validation.
- Check page budget. This section is currently long; prioritize operational relevance and validation hooks over narrative repetition.

### Proposed Approach: AI-discoverable and Crawlable Service Interfaces

Current fit:

- Strong connection to existing OPeNDAP/Hyrax behavior.
- Good practical framing around generic AI tools.
- The CMR virtual directory versus OPeNDAP virtual directory decision is important but currently reads like uncertainty without a decision process.

Plan:

- State the interface outcome concretely: an AI-crawlable, web-friendly view of OPeNDAP-enabled ESDIS collections.
- Add a decision point for which virtual directory implementation will be used, with criteria such as ESDIS approval, compatibility with generic AI tools, reuse by other OPeNDAP servers, and deployment effort.
- Replace "We have demonstrated (CITE?)" with a cited or documented result.
- Clean up wording: "reading extracting data" should become a clear description of how agents discover collections, inspect DAP4 metadata, and sample data.
- Tie this component to scoring: it improves Infrastructure and Access and establishes the path to operational deployment in Hyrax/EDC.

### Proposed Approach: AI-assisted Metadata Introspection and Validation

Current fit:

- This is the strongest AI-specific part of the proposal.
- The per-collection `usage.md` concept is concrete and reviewer-friendly.
- It needs clearer success criteria and stronger safeguards against hallucination.

Plan:

- Define the expected structure of `usage.md`: provenance, collection scope, variables, units, coordinate conventions, valid ranges, fill values, chunk/access guidance, known quirks, evidence links, confidence, and review status.
- Make the workflow explicit: select collection, sample granules, query CMR, query OPeNDAP/DAP4, inspect DMR++, run validators, compare findings, flag discrepancies, route to expert, publish approved guidance.
- Clarify how many collections or representative collection types will be used for prototype validation, if known. If not known, say selection will be made with ESDIS or DAAC partners.
- Add a plan for hallucination control: evidence-tagged claims, no unsupported assertions, deterministic checks, confidence labels, and expert review.
- Explain how generated metadata documents will be maintained over time, or explicitly scope maintenance as a path-to-operations issue.
- Avoid implying generated documents automatically correct CMR. The safer claim is that they surface discrepancies for expert review and possible downstream update.

### Proposed Approach: Machine-actionable Guidance for Autonomous Data Retrieval Workflows

Current fit:

- Good operational insight: guidance travels with DAP4 responses at the moment agents retrieve data.
- The value proposition is concrete: fewer failed requests, better subsetting, less guessing about units and coordinate conventions.
- The section repeats the `usage.md` concept and may need tightening.

Plan:

- Focus this part on integration: how Hyrax/DAP4 will expose approved guidance, what response shape changes, and how backward compatibility is preserved.
- Distinguish raw generated guidance from reviewed/approved guidance embedded in responses.
- Add acceptance criteria: agent can discover guidance in-band, issue a valid subset request, and avoid known failed access patterns in representative cases.
- Rewrite the listing into either a shorter example or a prose paragraph. The current listing is useful but consumes space and reads more like notes than proposal text.
- Fix the syntax issue in the example text around the empty units string.
- Keep the proof-of-concept, but make clear what was live-tested versus what is proposed for EDC.

### Limitations and Challenges

Current fit:

- The section is candid, which the call explicitly asks for.
- It names real risks: interface approval, rapidly changing agentic AI technology, CI/CD needs, and risk of misleading public documents.
- It should be more structured and should cover licensing/data-rights dependencies requested by the call.

Plan:

- Recast as risk plus mitigation pairs, while keeping it within about half a page.
- Include risks for:
  - ESDIS approval or choice of virtual directory implementation.
  - Agent/model reliability and hallucination.
  - External model/tool licensing, data rights, and platform dependence.
  - Security or prompt-injection risks from agent-facing service content.
  - DAAC bucket ownership and publication workflow.
  - Generated guidance becoming stale as collections change.
  - Page/scope risk given the 9- or 12-month project period.
- Add mitigation for each: fallback interface, deterministic validators, evidence tags, human review, open-source code, CI/CD, model abstraction, versioning, and ESDIS/DAAC decision gates.
- Remove informal phrasing such as "unknown unknowns" unless space allows and it is tied to a specific cohort-learning mitigation.

### Deliverables

Current fit:

- Three deliverables are listed and align with the three-part approach.
- Missing the call's mandatory final report and presentation/demo.
- Needs clearer "what exists at the end that does not exist today."

Plan:

- Reshape the list around concrete artifacts:
  - Working prototype or integration of AI-crawlable OPeNDAP/Hyrax directory access.
  - Agentic metadata introspection prototype with documented tools and tests.
  - Reviewed `usage.md` documents for selected collections or a clearly scoped representative set.
  - Hyrax/DAP4 integration path for exposing approved guidance.
  - Open-source repository or equivalent artifact with documentation.
  - Final report under 10 pages with validation results, lessons learned, and path to operations.
  - Presentation and technology demo for the Earth Data Officer and leadership team.
- Add acceptance evidence for each deliverable where possible.
- Avoid promising "all OPeNDAP-enabled data in ESDIS" unless the scope is validated against time and budget.
- Ensure documentation and tutorials are linked to open science requirements, not just described as nice-to-have extras.

### Validation and Path to Operations

Current fit:

- Empty, and therefore the largest scoring risk.
- The call directly asks: how will you know it works, who validates it, and what is needed for operational use.

Plan:

- Add a concise validation design with metrics:
  - Crawl coverage: percentage or count of target OPeNDAP-enabled collections discovered.
  - Metadata validation: number/type of discrepancies found, expert-confirmed precision, and false-positive handling.
  - Retrieval success: agents use guidance to issue correct subset requests in representative workflows.
  - Efficiency: reduced failed access attempts or improved chunk-aligned retrieval behavior.
  - Documentation and reproducibility: open repo, repeatable validation scripts, and archived test cases.
- Identify validators:
  - Ed Armstrong / PO.DAAC as domain expert, if confirmed.
  - ESDIS or DAAC partner reviewers for operational fit.
  - OPeNDAP engineering reviewers for Hyrax integration.
- Define gates to operations:
  - ESDIS agreement on virtual directory and DAP4 guidance exposure.
  - Security and data rights review.
  - Human review workflow for generated guidance.
  - CI/CD and monitoring for generated artifacts.
  - Open-source release and documentation.
- Include open science explicitly: code, docs, generated sample artifacts, and validation results should be public unless restricted by NASA policy.

### Timeline

Current fit:

- Part 1 has initial months.
- Parts 2 and 3 are mostly placeholders.
- Month 9 appears twice.
- The call allows up to 12 months and asks for month-by-month milestones, decision points, and final deliverable date.

Suggested plan:

- Decide whether the proposal is a 9-month or 12-month project. A 9-month project can work if scope is limited; a 12-month project gives more space for validation and path-to-operations work.
- If keeping 9 months:
  - Month 1: deploy/test virtual directory candidate and define target validation collections.
  - Month 2: choose VDI path with ESDIS guidance; verify crawlability and collection coverage.
  - Month 3: design agent workflow, evidence schema, and `usage.md` schema.
  - Month 4: implement initial CMR, OPeNDAP/DAP4, PyDAP/Xarray, and DMR++ tool calls.
  - Month 5: generate first `usage.md` artifacts for representative collections.
  - Month 6: run expert review and revise validators based on false positives/negatives.
  - Month 7: prototype DAP4 embedding or in-band guidance exposure in Hyrax.
  - Month 8: validate autonomous retrieval workflows and operational review path.
  - Month 9: package open-source artifacts, final report, and presentation/demo.
- Add decision points at Month 2, Month 6, and Month 8.
- Include a final deliverable date relative to project start once the start date is selected.

### Team

Current fit:

- Lists people, roles, and person-months.
- Includes PO.DAAC collaboration, which is important for eligibility and validation.
- Could better show capacity against the call's execution and budget scoring.

Plan:

- Align each person's role with the three work parts and validation:
  - James Gallagher: project lead, Hyrax/OPeNDAP architecture, agent workflow, software engineering.
  - Hannah Robertson: agent workflow implementation, validators, tests, documentation.
  - Ed Armstrong: DAAC/domain validation, PO.DAAC operational feedback, representative collection selection.
- Add any required ESDIS/DAAC dependency that is not a funded team member but is needed for deployment decisions.
- Confirm person-month totals against the budget summary.
- If institutional authorization or funded team lead status needs to be explicit for eligibility, add it here or in the metadata.

### Budget Summary

Current fit:

- Empty.
- The call expects a high-level breakdown and says covered costs include personnel, compute, and tooling. Hardware procurement and travel should not be included unless justified.

Plan:

- Add the requested funding amount once chosen, likely within the call's expected $150,000 to $200,000 range.
- Break down by:
  - Personnel by role/person-month.
  - Compute/model/API costs for development and validation.
  - Tooling or cloud storage costs, if any.
  - Indirect costs, if applicable under existing terms.
- State that no hardware procurement is requested, unless the team truly needs it.
- State whether travel is excluded or justified.
- Tie budget categories directly to deliverables so reviewers can see scope realism.

## Cross-Cutting Cleanup Plan

- Remove red template prompt text before final PDF submission.
- Remove or rewrite internal notes and placeholder comments visible in compiled text.
- Replace `CITE?` placeholders with citations or remove the claim.
- Check LaTeX formatting for Markdown artifacts such as `*emphasis*`, backticks, and listing content.
- Ensure terms are defined once and used consistently: EDC, ESDIS, DAAC, DAP4, DMR++, CMR, VDI, `usage.md`.
- Keep all claims defensible. Where proof-of-concept results are mentioned, name what was tested and what evidence exists.
- Review page count early. The proposal is already text-heavy, and the validation and budget sections still need space.
- Make each section point back to the rubric: strategic alignment, AI justification, operational relevance, validation/open science, and team/budget fit.
