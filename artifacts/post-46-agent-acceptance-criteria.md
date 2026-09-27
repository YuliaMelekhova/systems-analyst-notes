<!-- LinkedIn: -->

# Agent Acceptance Criteria Template

**Series:** Systems Analyst Notes
**Post:** 46
**Phase:** 6 AI Agents at Work
**Author:** Yulia Melekhova
**Published:** 2026

## Purpose

Names the four values that must be agreed before an agent task type ships, the six metrics that define them, and the evaluation set discipline that makes a score reproducible. Fill in one row per task type, not one row per agent.

---

## 1. Why task type, not agent

A single agent doing three jobs needs three thresholds. A 90% success rate is acceptable for a draft. For a compliance flag that gates a payment, it is not. Writing one threshold for the agent as a whole averages across jobs that should never share a ceiling.

The Finance Agent benchmark makes this concrete: the best-performing model scored 63.3% on tasks typical of an entry-level financial analyst. A 37% error rate is unacceptable in any workflow where output reaches a customer document or a regulatory record. The number itself is not the problem. The problem is that most teams never wrote down what number they would refuse to ship against, so there is nothing to compare it to.

---

## 2. Four fields per task type

| Field | What to write |
|---|---|
| Metric | Which of the six metrics (Section 3) defines success for this task type |
| Threshold | The measured value below which this task does not ship. A specific number, not a range |
| Review policy | What happens to outputs between the threshold and perfect: auto-proceed, sampled review at a stated percentage, or review every output |
| Owner | The named person who makes the go/no-go call when the measured number lands under the threshold |

The owner field is the one most templates leave blank. "The team decides" is not an owner.

---

## 3. Six metrics

**Success rate.** Tasks completed end to end, without manual intervention. The baseline metric.

**Tool accuracy.** Correct tool selected, correct parameters passed. An agent that reaches the right answer by calling the wrong tool or guessing a parameter has a fragile path the next task will break.

**Trajectory evaluation.** Coherent reasoning path, even when the final answer is correct. A correct answer reached by an incoherent path is a future incident. The path is what the audit reconstructs when something goes wrong.

**Latency against SLA.** Response time at the agreed percentile. p95 is the standard measure; p99 matters for any step in a customer-facing flow.

**Availability of required services.** The fraction of task attempts where every tool the agent depends on was reachable. An agent that cannot be evaluated because a dependency was down is not ready for a production SLA.

**Retry-and-failure rate with recovery logged.** How often the agent retried, and whether each retry and its outcome was captured. An agent that retries silently has no audit trail for the runs that cost twice.

---

## 4. The acceptance criteria table

One row per task type. Add rows as the agent takes on new jobs.

| Task Type | Metric | Threshold | Review Policy | Model Version | Owner |
|---|---|---|---|---|---|
| Requirement draft | Success rate | > 85% | Sampled review at 20% | `[pin version]` | SA lead |
| Compliance flag | Tool accuracy | > 97% | Review every output | `[pin version]` | Risk owner |
| ADR summary | Trajectory eval | > 90% | Sampled review at 30% | `[pin version]` | Arch lead |
| Status update (write) | Latency vs. SLA | < 5s p95 | Auto-proceed | `[pin version]` | DevOps |
| API contract check | Retry/fail rate | < 3% retries | Review every output | `[pin version]` | API owner |

**Model Version field:** The evaluation record must pin the model version alongside the score. If the vendor retires the version, the recorded number no longer corresponds to anything reproducible. A score without a pinned version is an anecdote with a date on it.

---

## 5. The evaluation set

The evaluation set is the artifact, not the score.

A score without a fixed test set is a claim about one afternoon. The requirement is a versioned set of representative tasks with known-good outputs, held stable across model versions. When the score changes, that should mean the system changed - not just what was asked.

**Minimum viable evaluation set per task type:**

- 20+ representative tasks drawn from production or realistic synthetic scenarios
- A known-good output for each task, reviewed and approved by a domain expert
- A development set the team can examine during tuning
- A holdout set that stays unseen during tuning. Without the split, the evaluation set turns into training data for the prompt, and the measured number stops describing what a new, unseen request will get.

**Annotation flywheel:** Every rejected agent output in production becomes a new case in the evaluation set. A system without this loop is frozen at the quality of its first deployment. The evaluation set stops describing production within weeks unless rejections feed it continuously.

---

## 6. The judge model

The evaluation set needs something to score it. A judge model evaluating each case honestly needs four inputs:

1. The original request
2. The source material the agent had access to at the time
3. The agent output
4. A written rubric naming the dimensions that matter for this task type

Scoring without source material turns the judge into a fluency checker. A fluent but factually wrong answer passes. A correct but terse one fails. That is not an acceptance criterion - it is a style preference.

**Four verdict structures, matched to gate type:**

| Structure | Best for | Limitation |
|---|---|---|
| Point scoring (1-5 per dimension) | Tracking drift over time | Needs a written definition per point value or scores are arbitrary |
| Pass / fail | Hard deployment gate | Hides a score sliding from excellent to barely passing |
| Pairwise comparison vs. production baseline | Calibration | More reliable than absolute scoring; judge identifies which of two is better |
| Error identification | Development phase | Names the specific unsupported claim; explains a score change |

**Calibration step:** A judge is not trustworthy by default. Pull a sample the judge scored. Have a domain reviewer score the same sample blind. Measure agreement. That exercise reveals whether the threshold is too strict, too lenient, or missing a failure category entirely - before the threshold goes into a shipping gate.

**Independence rule:** A judge from the same model family as the generator shares the same training data and the same blind spots. For any task type where the review policy is "AI reviews AI," document what makes the reviewer genuinely independent of the generator, or the review policy column is decorative.

---

## 7. The filter stack

Between the threshold and perfect, the review policy is not a single gate. A stack of four filters, each cheaper than the one below it, covers blind spots the one above it cannot see:

1. Schema check - catches malformed structure for near-zero cost
2. Deterministic test - catches wrong answers a schema check cannot see
3. Human review - catches what no automated check can
4. Production monitoring - catches whatever passed the first three

A filter tuned to catch everything drowns reviewers in false positives. A reviewer trained by too many false escalations stops reading carefully. Both outcomes quietly turn the review gate into a rubber stamp.

---

## 8. Review gate for shipping

Five checks before any agent task type ships to production.

1. Is there a row in the acceptance criteria table for this task type, with all four fields filled?
2. Does the evaluation set exist, with a development and holdout split?
3. Is the model version pinned in the evaluation record?
4. Has the judge model been calibrated against a domain reviewer on a representative sample?
5. Is there a named owner for the go/no-go decision when the score lands under the threshold?

A task type that passes all five is ready. A task type that passes four and skips the owner field has an acceptance criterion nobody can enforce.

---

## Related Artifacts

- [artifacts/post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md) - Pre-launch checklist this template gates; the seven-parameter instruction standard the agent was specified against
- [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) - The checkpoint tiers the review policy column maps to; five-tier structure from auto-proceed to kill switch
- [artifacts/post-48-loop-engineering-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-48-loop-engineering-spec.md) - Where every rejected output in the annotation flywheel gets its stop condition defined

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
