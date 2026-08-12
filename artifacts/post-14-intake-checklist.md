<!-- LinkedIn: https://www.linkedin.com/posts/yuliamelekhova_systemsanalysis-businessanalysis-requirements-share-7489594821527928832-bUqS/ -->

# Requirement Intake Checklist

Series: Systems Analyst Notes
Post: 14
Phase: 3 Building the Foundation
Author: Yulia Melekhova
Published: 2026

## Purpose

A two-stage filter that runs before a requirement gets written. Stage 1 checks whether the inputs exist at all, and Stage 2 checks whether the requirement is understood well enough to document.

Documenting a requirement that fails the pre-checklist is waste. The document gets rewritten anyway once the missing input surfaces.

---

## Stage 1: Pre-Checklist

Is this ready to document? Work through all four gates before writing anything. A single "No" means stop and resolve it first.

| # | Gate | Pass / Fail | Notes |
|---|------|-------------|-------|
| 1 | **Acceptance criteria defined:** specific, testable conditions exist, not gestured at | | |
| 2 | **Dependencies mapped:** upstream requirements, API contracts or data sources identified | | |
| 3 | **Product owner sign-off on goal:** confirmed in writing, not only verbally in a standup | | |
| 4 | **Team capacity confirmed:** no unresolved spillover from the previous sprint blocking this work | | |

All four pass, then proceed to Stage 2.

---

## Stage 2: Three Questions

These aren't sequential steps. A requirement can fail question 1 and pass question 3. Work through all three independently.

### Question 1: Who uses this output, and how?

Name the specific user, system or downstream process that consumes this requirement's output.

* If the answer is vague ("the team," "various stakeholders"), the requirement is still at concept stage.
* Concepts don't belong in a requirements document.

| Field | Answer |
|-------|--------|
| Consumer (user / system / process) | |
| How they consume the output | |
| Frequency / trigger | |

---

### Question 2: What happens if this fails?

Describes the real risk level. Honest priority assignment depends on this answer.

* If the answer is "not much," revisit the priority before writing the requirement.
* If the answer involves compliance, customer funds, regulatory reporting or a partner-facing SLA, flag for compliance review before Stage 1 closes.

| Field | Answer |
|-------|--------|
| Failure mode | |
| Business impact | |
| Compliance / regulatory exposure | |
| Priority justified? (Y / N / Needs review) | |

---

### Question 3: How will we know it's working?

The measurable signal. No measurement means no acceptance criteria, only intent stated confidently.

* Intent and acceptance criteria look identical until implementation. Then they don't.
* If this field is empty, the requirement is not ready to write.

| Field | Answer |
|-------|--------|
| Success metric / observable signal | |
| Who verifies it | |
| When verification occurs | |

---

## Outcome

| Pre-checklist | Q1 | Q2 | Q3 | Status |
|---------------|----|----|-----|--------|
| All pass | Named | Risk assessed | Metric defined | Ready to write |
| Any fail | n/a | n/a | n/a | Stop. Resolve gap. |
| All pass | Vague | n/a | n/a | Return to discovery |
| All pass | Named | "Not much" | n/a | Revisit priority |
| All pass | Named | Assessed | Empty | Not ready. Define measurement. |

---

## Usage notes

* Run once per user story or requirement before drafting begins.
* If the PO is also the approver, which is common in small teams, make that explicit in the sign-off field.
* For cross-border fintech, add a fifth pre-checklist gate: **jurisdiction confirmed.** Which market does this requirement apply to, and is the applicable compliance constraint identified?
* Keep the completed checklist next to the requirement rather than in a separate folder. It is the record of why the requirement was accepted, and it answers the question an auditor asks six months later.

---

## Related Artifacts

* [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) - Where a requirement goes when Question 1 sends it back to discovery
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Turns the failure mode from Question 2 into mapped paths
* [templates-quality-rules/readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) - The gates that run at review, where this checklist runs before drafting
* [knowledge-packs/iso-20022-cbpr-plus.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/iso-20022-cbpr-plus.md) - A worked case for the jurisdiction gate, with a hard deadline attached to it
* [artifacts/post-10-tribal-knowledge-signs.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-10-tribal-knowledge-signs.md) - Why the sign-off gate exists in the first place

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
