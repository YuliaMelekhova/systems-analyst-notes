# Systems Analyst Notes — Companion Artifacts

This repo holds the companion artifacts behind the "Systems Analyst Notes"
series: templated versions of an AI Documentation Framework (ADF), built
around the kind of system a cross-border fintech company runs on. Each
artifact is a working template, shaped the way a real document for that
kind of system would be, then generalized enough to reuse.

## Structure

The framework has five branches.

**Knowledge Packs** — reference material on the standards this system
touches: BABOK, OpenAPI, ISO 20022, Open Banking Standards, RFC 9110 and
related RFCs, Microsoft Manual of Style. Each pack is written up once and
reused across every relevant requirement instead of re-researched each time.

**STRIDE Threat Modeling** — threat modeling artifacts cross-linked to the
requirements and API specs they apply to, instead of sitting in a separate
security silo nobody checks during requirement work.

**Governance Matrix** — a mapping of which regulatory framework applies in
which market: EU AI Act, NIST AI RMF, ISO/IEC 42001, LGPD, LFPDPPP, Law
1581/2012, and how they overlap.

**Prompt Library** — prompts shaped for common analytical tasks, kept as
reusable references instead of rewritten from scratch every time.

**Templates & Quality Rules** — the actual artifact templates (BRD, SRS, ADR,
API contracts, decision tables) plus the naming and readiness rules that
decide when a document is ready for review.

## Artifacts published so far

| Post | Title | Phase | File |
|---|---|---|---|
| 7 | Documentation Is Organizational Memory | 2 — The Knowledge Chapter | this README |
| 10 | Six Signs Tribal Knowledge Is Becoming Dangerous | Phase 2 | [artifacts/post-10-tribal-knowledge-signs.md](artifacts/post-10-tribal-knowledge-signs.md) |
| 12 | Knowledge Graph — Mapping How Information Actually Connects | Phase 2 | [artifacts/post-12-knowledge-graph.mmd](artifacts/post-12-knowledge-graph.mmd) |

More rows get added here as `[GitHub]`-tagged posts in the series ship.

## How this repo works

Each companion artifact lives in `/artifacts`, named `post-NN-slug.ext`,
matching the post number in the LinkedIn series. See `github_repo_guide.md`
(kept outside this repo, in the content project) for the full naming and
formatting convention.

---

*Companion repo to the "Systems Analyst Notes" series on LinkedIn.*
