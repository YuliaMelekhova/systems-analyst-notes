<!--
Post: 18
Title: My 5-Step Discovery Framework
Phase: 3 - Building the Foundation
LinkedIn: https://www.linkedin.com/posts/yuliamelekhova_systemsanalysis-requirementsdiscovery-baframework-share-7492128085102809088-XosY/?utm_source=social_share_send&utm_medium=member_desktop_web&rcm=ACoAABW2QzcBN4fI21bG0ls7u2nHq-ooXTFxjEU
-->

# 5-Step Discovery Framework

**Series:** Systems Analyst Notes  
**Post:** 18  
**Phase:** 3 Building the Foundation  
**Author:** Yulia Melekhova  
**Published:** 2026  

---

## Purpose

Not every requirement earns the same depth of discovery. This framework includes a triage gate (Step 0) that runs before the five steps begin, so discovery effort scales with what is actually at stake.

---

## Step 0 - Triage Gate

Before discovery begins, classify the requirement by priority tier. A quick show of hands across the team is often enough. Formal estimation is not required here - the goal is to calibrate effort, not produce a project plan.

| Tier | Label | Discovery depth |
|------|-------|----------------|
| 1 | Critical | Full 5-step discovery |
| 2 | Important | Steps 1-4, abbreviated Step 5 |
| 3 | Nice-to-have | Steps 1-2 only |
| 4 | Not now | Document and defer |

When the triage phase reveals conflicting priorities or uncertain value, that is a signal to slow down and add a prioritization exercise. The scope can range from a quick MoSCoW sort to a full cost-of-delay analysis, depending on how much is known about business impact.

---

## Step 1 - Understand the Business Goal

**Question:** What outcome does the business need?

Not the feature - the result. The requirement exists to serve a goal. If you cannot write the success metric for that goal in one sentence, you have not found it yet.

**Checklist:**
- [ ] Can you state the desired business outcome in measurable terms?
- [ ] Does the product owner agree with that statement?
- [ ] Is there a success metric, deadline, or threshold that defines "done" at the business level?

---

## Step 2 - Map the Context

**Question:** Who initiates this, who is affected downstream, and what systems touch it?

Draw the boundary before writing a single requirement. The context diagram (system boundary + external actors) is the output of this step, not a later deliverable.

**Checklist:**
- [ ] Are all external systems named and their interfaces described?
- [ ] Are all user roles identified (initiator, affected parties, approvers)?
- [ ] Is the boundary between in-scope and out-of-scope explicit?
- [ ] For fintech: are all message types and corridors named (e.g., pacs.008, CBPR+, specific currency corridors)?

---

## Step 3 - Identify Constraints

**Question:** What cannot change, and what is fixed before the requirement is written?

Constraints that surface here cost nothing. Constraints discovered in UAT cost months. Categories to check: regulatory, technical, timeline, budget, organizational, and contractual.

**Checklist:**
- [ ] Regulatory: which jurisdictions apply, which standards govern this feature?
- [ ] Technical: what existing systems must this integrate with, and what are their limits?
- [ ] Timeline: are there hard deadlines (regulatory, contractual, market)?
- [ ] Organizational: who must sign off, and what approval cycle does that require?

---

## Step 4 - Discover the Unhappy Paths

**Question:** What fails, and what does the system do when it fails?

The happy path describes intended behavior. Unhappy paths describe what happens at every failure mode, compliance gate, and boundary condition. For fintech requirements, this includes: what happens when data is missing, when a threshold is crossed, when two regulatory regimes conflict, when a downstream system rejects the message.

**Checklist:**
- [ ] Are the top five failure modes named?
- [ ] Does each failure mode have a specified system response?
- [ ] Are compliance failure paths documented separately from functional failure paths?
- [ ] For cross-border payments: are Travel Rule, AML hold, and sanctions screening unhappy paths mapped?

---

## Step 5 - Show-Stopper Check

**Question:** Does anything here block delivery or violate a hard constraint?

One final pass before baselineThis step does not require formal sign-off; it requires one honest answer. If anything fails this check, the requirement does not go to baseline until it is resolved.

**Show-stopper conditions:**
- [ ] A hard regulatory deadline that the current scope cannot meet
- [ ] A dependency on a system or team that is unavailable or unconfirmed
- [ ] A conflicting requirement already baselined in a prior sprint
- [ ] A missing product owner decision that the requirement assumes has been made

---

## When to Add a Prioritization Exercise

The triage gate (Step 0) may not produce a clear answer. When it reveals conflicting priorities or uncertain business value, add a prioritization exercise between Step 0 and Step 1.

**Options by complexity:**

| Situation | Tool |
|-----------|------|
| Low uncertainty, small team | MoSCoW sort (10 minutes) |
| Competing features, known cost | Value vs. effort matrix |
| Hard deadline, revenue at risk | Cost-of-delay analysis |
| Multi-stakeholder disagreement | Weighted scoring with explicit criteria |

The purpose is not to produce a perfect ranking - it is to surface the assumptions behind conflicting priorities and name them explicitly before discovery effort is spent.

---

## Related Artifacts

* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - The pre-checklist that decides whether discovery is worth starting
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - The full framework behind Step 4
* [templates-quality-rules/readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) - The gates that decide whether the discovery output can go to review

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova

