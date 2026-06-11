# Abstract Draft

NASA Earth Science Data Systems (ESDS) manages more than 180 petabytes of Earth
science data, with holdings expected to exceed 600 petabytes by the early
2030s. At that scale, metadata records, access guidance, and cloud-optimization
artifacts can drift from the data products they describe, increasing failed
discovery, failed first attempts at access, and manual curation burden. This
project will extend OPeNDAP/Hyrax in the Earthdata Cloud with AI-crawlable
service interfaces and an agentic metadata-introspection workflow that helps
make NASA data easier for both people and autonomous tools to find, understand,
and use.

The proposed system will use a model-agnostic AI agent to coordinate
deterministic calls to the Common Metadata Repository (CMR), OPeNDAP/Hyrax,
PyDAP, and DMR++ resources. For selected representative collections, the
workflow will traverse collection structure, inspect authoritative metadata and
Data Access Protocol 4 (DAP4) responses, sample representative granules, check
units, coordinates, fill values, valid ranges, chunk structure, and
cross-granule consistency, and draft evidence-linked collection-level `usage.md`
documents. Each generated claim will carry provenance, confidence, and review
status, and will be labeled as stated, inferred, uncertain, or unsupported.
Unsupported claims will be omitted or routed for expert review; the system will
not modify CMR records or other Earthdata Cloud artifacts.

The project advances the ESDS Infrastructure and Access pillars by improving
existing machine-readable services rather than creating a new portal. Its
deliverables include a working AI-crawlable Virtual Directory Interface
prototype, a set of `usage.md` guidance documents stored in an OPeNDAP-managed
S3 bucket, and an open-source metadata-introspection repository with schemas,
workflow configuration, validators, tests, documentation, and reproducibility
notes. The result will be a validated path toward agent-ready OPeNDAP access
that preserves human oversight, exposes uncertainty, and supports future
operational adoption by NASA data systems.
