<!--
Post: 14
Title: 3 Questions I Ask Before Writing Any Requirement
Phase: 3 — Building the Foundation
LinkedIn: [https://www.linkedin.com/posts/yuliamelekhova_systemsanalysis-businessanalysis-requirements-share-7489594821527928832-bUqS/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABW2QzcBN4fI21bG0ls7u2nHq-ooXTFxjEU]
-->

# Requirement Intake Checklist

A two-stage filter. Run the pre-checklist first. If it passes, apply the three questions.
Documenting a requirement that fails the pre-checklist is waste — the document will need
to be rewritten once the missing input surfaces.

---

## Stage 1: Pre-Checklist — Is This Ready to Document?

Work through all four before writing anything. A single "No" means stop and resolve it first.

| # | Gate | Pass / Fail | Notes |
|---|------|-------------|-------|
| 1 | **Acceptance criteria defined** — not gestured at; specific, testable conditions exist | | |
| 2 | **Dependencies mapped** — upstream requirements, API contracts, or data sources identified | | |
| 3 | **Product owner sign-off on goal** — confirmed in writing, not only verbally in a standup | | |
| 4 | **Team capacity confirmed** — no unresolved spillover from previous sprint blocking this work | | |

If all four pass → proceed to Stage 2.

---

## Stage 2: Three Questions

These aren't sequential steps. A requirement can fail question 1 and pass question 3.
Work through all three independently.

### Question 1: Who uses this output, and how?

Name the specific user, system, or downstream process that consumes this requirement's output.

- If the answer is vague ("the team," "various stakeholders"), the requirement is still at concept stage.
- Concepts don't belong in a requirements document.

| Field | Answer |
|-------|--------|
| Consumer (user / system / process) | |
| How they consume the output | |
| Frequency / trigger | |

---

### Question 2: What happens if this fails?

Describes the real risk level. Honest priority assignment depends on this answer.

- If the answer is "not much," revisit the priority before writing the requirement.
- If the answer involves compliance, customer funds, or regulatory reporting — flag for compliance review before Stage 1.

| Field | Answer |
|-------|--------|
| Failure mode | |
| Business impact | |
| Compliance / regulatory exposure | |
| Priority justified? (Y / N / Needs review) | |

---

### Question 3: How will we know it's working?

The measurable signal. No measurement = no acceptance criteria, just intent stated confidently.

- Intent and acceptance criteria look identical until implementation. Then they don't.
- If this field is empty, the requirement is not ready to write.

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
| Any fail | — | — | — | Stop. Resolve gap. |
| All pass | Vague | — | — | Return to discovery |
| All pass | Named | "Not much" | — | Revisit priority |
| All pass | Named | Assessed | Empty | Not ready — define measurement |

---

## Usage notes

- Run once per user story or requirement before drafting begins.
- If the PO is also the approver (common in small teams), make that explicit in the sign-off field.
- For cross-border fintech: add a fifth pre-checklist gate — **jurisdiction confirmed** (which market
  does this requirement apply to, and is the applicable compliance constraint identified?).
