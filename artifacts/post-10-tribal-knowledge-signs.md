<!--
Post: 10
Title: Six Signs Tribal Knowledge Is Becoming Dangerous
Phase: 2 — The Knowledge Chapter
LinkedIn: [link once published]
-->

# Six Signs Tribal Knowledge Is Becoming Dangerous

A scored checklist for identifying knowledge risk in fast-growing teams.
Each sign carries a weight (1–3). Score your team honestly.
**Total 14+ = structural knowledge risk. Act before a resignation forces the issue.**

---

## The Seven Signs

### Sign 1 — Critical decisions require a specific person to be online
**Weight: 2**

No document explains the decision. No record shows the reasoning. One person carries it, and when they're in a meeting, unavailable, or gone, work stops.

**How to check:** Ask a developer or PM to explain the rationale behind a key architectural or product decision. If the answer is "you'd have to ask [name]," this sign is present.

Score: ☐ 0 (not present) ☐ 1 (occasionally) ☐ 2 (regularly)

---

### Sign 2 — New team members spend their first month asking questions instead of contributing
**Weight: 1**

The onboarding isn't broken. The knowledge was never written down to begin with.

**How to check:** Track how long it takes a new hire to submit their first independent deliverable. If it's longer than 3 weeks and requires constant guidance from senior staff, this sign is present.

Score: ☐ 0 (not present) ☐ 1 (present)

---

### Sign 3 — The same architectural question gets answered differently depending on who you ask
**Weight: 2**

Two developers, two founders, four different answers. Each one confident. None of them aware of the inconsistency.

**How to check:** Ask the same question to two people independently: "What is our approach to [X]?" Compare answers. Inconsistency = no single source of truth.

Score: ☐ 0 (consistent answers) ☐ 1 (minor inconsistencies) ☐ 2 (significant contradictions)

---

### Sign 4 — Post-mortems keep surfacing "we didn't know that rule existed"
**Weight: 3**

Not a testing gap. A documentation gap that looked like a testing gap after the incident.

**How to check:** Review the last 3 post-mortems or incident reports. Count how many root causes trace back to undocumented rules, constraints, or decisions rather than code bugs.

Score: ☐ 0 (not present) ☐ 1 (appeared once) ☐ 2 (appeared twice) ☐ 3 (recurring pattern)

---

### Sign 5 — Slack is the de facto specification system
**Weight: 2**

The requirement lives in a thread from six months ago. The developer who wrote it has since left. The thread has 47 replies and no summary.

**How to check:** When a developer needs to verify a requirement, where do they go first? If the answer is Slack search rather than a spec document, this sign is present.

Score: ☐ 0 (not present) ☐ 1 (occasionally) ☐ 2 (this is the primary pattern)

---

### Sign 6 — The team can't onboard a contractor without one of the founders sitting in
**Weight: 2**

Every new person needs a guided tour from someone irreplaceable. That's not a hiring problem. It's a knowledge architecture problem.

**How to check:** Could you onboard a new contractor or analyst using only written documentation, without a live walkthrough from a founder or senior engineer?

Score: ☐ 0 (yes, documentation covers it) ☐ 1 (partial — some live guidance needed) ☐ 2 (no — impossible without a guided session)

---

### Sign 7 — The people who built the AI can explain it, but no document can
**Weight: 3**

Governance gaps — missing records of why a model was configured a certain way, who approved a specific threshold, what the rollback process looks like — are no longer just documentation debt. A Grant Thornton survey in 2026 found 78% of business executives couldn't pass an independent AI governance audit within 90 days. The most common gap wasn't missing technology. It was missing records of how decisions were made. Regulators are now signaling that documentation gaps themselves may constitute violations, not just the missing control but the missing record of why that control was chosen.

**How to check:** Pick any decision made about your AI system in the last six months — a model choice, a threshold setting, a data exclusion. Is there a written record of who made that decision, what alternatives were considered, and why this option was selected? If the answer lives only in someone's memory, this sign is present.

Score: ☐ 0 (not present) ☐ 1 (partial records exist) ☐ 2 (decisions undocumented but traceable) ☐ 3 (no records; knowledge is person-dependent)

---

## Scoring

| Total score | Risk level | Recommended action |
|---|---|---|
| 0–3 | Low | Monitor. Document decisions as they happen. |
| 4–8 | Moderate | Run a knowledge audit. Identify the two highest-weight gaps and address them first. |
| 9–13 | High | Assign ownership. Build a documentation backlog. Start with the single highest-weight sign. |
| 14+ | Critical | Structural knowledge risk. One resignation could cost months of recovery time. Treat as a project, not a task. |

---

## Where to start

If you scored 9 or above, prioritize by weight, not by ease.

Signs weighted 3 (Signs 4 and 7) compound fastest — undocumented rules cause incidents, and undocumented AI governance decisions are now a regulatory exposure. Signs weighted 2 (Signs 1, 3, 5, 6) affect daily velocity and onboarding continuously. Sign weighted 1 (Sign 2) is a symptom; fixing it without addressing the higher-weight signs doesn't resolve the root cause.

Sign 7 deserves specific attention for teams building or operating AI systems: the documentation gap it describes is no longer just an operational risk. As of 2026, regulators are treating missing governance records as a compliance issue in their own right. If your team scores 3 on Sign 7, that gap should be treated as a project with a deadline, not a backlog item.

The goal isn't a documentation sprint. It's a decision about which knowledge the company can afford to leave unwritten — and building the minimum structure that makes the rest findable.
