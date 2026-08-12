<!-- LinkedIn: https://www.linkedin.com/posts/yuliamelekhova_systemsanalysis-knowledgemanagement-fintech-share-7487021286582403072-yWuY/ -->

# Seven Signs Tribal Knowledge Is Becoming Dangerous

Series: Systems Analyst Notes
Post: 10
Phase: 2 The Knowledge Chapter
Author: Yulia Melekhova
Published: 2026

## Purpose

A scored checklist for measuring how much of a team's operating knowledge lives in people rather than in writing. Run it before a resignation forces the question, and use the weights to decide which gap gets closed first.

Each sign carries a weight of 1 to 3. Score honestly.
**Total 14 or above means structural knowledge risk.**

---

## The Seven Signs

### Sign 1: Critical decisions require a specific person to be online
**Weight: 2**

No document explains the decision. No record shows the reasoning. One person carries it, and when they're in a meeting, unavailable, or gone, work stops.

**How to check:** Ask a developer or PM to explain the rationale behind a key architectural or product decision. If the answer is "you'd have to ask [name]," this sign is present.

Score: ☐ 0 (not present) ☐ 1 (occasionally) ☐ 2 (regularly)

---

### Sign 2: New team members spend their first month asking questions instead of contributing
**Weight: 1**

The onboarding process is fine. The knowledge behind it was never written down.

**How to check:** Track how long it takes a new hire to submit their first independent deliverable. If it's longer than 3 weeks and requires constant guidance from senior staff, this sign is present.

Score: ☐ 0 (not present) ☐ 1 (present)

---

### Sign 3: The same architectural question gets answered differently depending on who you ask
**Weight: 2**

Two developers, two founders, four different answers. Each one confident. None of them aware of the inconsistency.

**How to check:** Ask the same question to two people independently: "What is our approach to [X]?" Compare answers. Inconsistency means there is no single source of truth.

Score: ☐ 0 (consistent answers) ☐ 1 (minor inconsistencies) ☐ 2 (significant contradictions)

---

### Sign 4: Post-mortems keep surfacing "we didn't know that rule existed"
**Weight: 3**

A documentation gap that looked like a testing gap until someone read the incident report closely.

**How to check:** Review the last 3 post-mortems or incident reports. Count how many root causes trace back to undocumented rules, constraints, or decisions rather than code bugs.

Score: ☐ 0 (not present) ☐ 1 (appeared once) ☐ 2 (appeared twice) ☐ 3 (recurring pattern)

---

### Sign 5: Slack is the de facto specification system
**Weight: 2**

The requirement lives in a thread from six months ago. The developer who wrote it has since left. The thread has 47 replies and no summary.

**How to check:** When a developer needs to verify a requirement, where do they go first? If the answer is Slack search rather than a spec document, this sign is present.

Score: ☐ 0 (not present) ☐ 1 (occasionally) ☐ 2 (this is the primary pattern)

---

### Sign 6: The team can't onboard a contractor without one of the founders sitting in
**Weight: 2**

Every new person needs a guided tour from someone irreplaceable. That points at knowledge architecture rather than hiring.

**How to check:** Could you onboard a new contractor or analyst using only written documentation, without a live walkthrough from a founder or senior engineer?

Score: ☐ 0 (yes, documentation covers it) ☐ 1 (partial, some live guidance needed) ☐ 2 (no, impossible without a guided session)

---

### Sign 7: The people who built the AI can explain it, but no document can
**Weight: 3**

Governance gaps carry a different cost than they used to. Missing records of why a model was configured a certain way, who approved a specific threshold, and what the rollback process looks like are no longer ordinary documentation debt. A Grant Thornton survey in 2026 found 78% of business executives couldn't pass an independent AI governance audit within 90 days. The most common gap was missing records of how decisions were made rather than missing technology. Regulators are now signaling that a documentation gap may constitute a violation on its own, separate from the control it fails to describe.

**How to check:** Pick any decision made about your AI system in the last six months: a model choice, a threshold setting, a data exclusion, a vendor swap. Is there a written record of who made that decision, what alternatives were considered, and why this option was selected? If the answer lives only in someone's memory, this sign is present.

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

If you scored 9 or above, prioritize by weight rather than by ease.

Signs weighted 3 compound fastest. Undocumented rules cause incidents, and undocumented AI governance decisions are now a regulatory exposure. Signs weighted 2 affect daily velocity and onboarding continuously. The sign weighted 1 is a symptom, and fixing it while the higher-weight signs stay open leaves the root cause untouched.

Sign 7 deserves specific attention for teams building or operating AI systems. The gap it describes has moved beyond operational risk. As of 2026, regulators are treating missing governance records as a compliance issue in their own right. A score of 3 on Sign 7 belongs in the roadmap with a deadline attached, not in a backlog.

The output of this checklist is a decision about which knowledge the company can afford to leave unwritten, plus the minimum structure that makes the rest findable.

---

## Related Artifacts

* [artifacts/post-12-knowledge-graph.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-12-knowledge-graph.md) - Maps the dependency chain that Signs 1, 3 and 4 leave invisible
* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - Stops new requirements from adding to the undocumented pile

---

Systems Analyst Notes · [github.com/yuliamelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
