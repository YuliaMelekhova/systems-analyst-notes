<!-- LinkedIn: -->

# Loop Engineering Spec Template

**Series:** Systems Analyst Notes
**Post:** 48
**Phase:** 6 AI Agents at Work
**Author:** Yulia Melekhova
**Published:** 2026

## Purpose

Provides the per-step stop conditions table, the read-only vs. write risk tier classification, and the restart and idempotency rules that separate a well-specified agent loop from an unbounded production defect. Fill in one row per pipeline step before any agent is built.

---

## 1. Why loops need specifications, not intentions

At 95% success per step, ten chained steps deliver a correct result 60% of the time. At twenty steps, that falls to 36%. This is not a model quality problem. It is a structural property of any chained system.

An unbounded loop is a production defect, not a gap discovered in staging. Retrying without new evidence buys another version of the same uncertainty at full cost.

The stop condition for each step is a requirement, not an implementation detail. It belongs in the spec alongside the step's job description.

---

## 2. Per-step stop conditions table

One row per step. Every field is required. An empty cell means the step will run until it exhausts compute or context.

| Step | Max Iterations | Token Budget | Retry Budget | Confidence Threshold | Validation Gate | Escalation Path |
|---|---|---|---|---|---|---|
| Research | 3 | 2,000 / step | 2 retries | 0.80 | Source found + chunked | Route to lighter source |
| Drafting | 4 | 4,000 / step | 1 retry | 0.82 | Schema validates | Flag for human review |
| Validation | 2 | 1,500 / step | 1 retry | 0.88 | Draft matches source | Block + notify owner |
| `[add step]` | `[N]` | `[N tokens]` | `[N retries]` | `[0.NN]` | `[named rule]` | `[named path]` |

**Escalation path field:** Name the specific action, not "escalate." "Route to lighter source," "flag for human review," and "block and notify owner" are named actions. "Handle appropriately" is not.

**Confidence threshold:** When the agent's own confidence estimate falls below this value, the step stops and escalates rather than retrying. The threshold must be lower than the acceptance criteria threshold for this task type - a step that keeps running past its confidence floor produces an artifact that looks done and is not.

---

## 3. The restart policy

Two restart policies apply, and they are not interchangeable.

**Discard and restart from original input.**
When a step fails, discard every completed output for that step and restart using only the original input. This eliminates the coupling between the failed state and the next attempt. American Express uses this principle in card authorization: when a service fails mid-transaction, the orchestrator restarts from the original transaction input in a healthy cell, not from the partial state left by the failed one.

**Resume from checkpoint.**
When a step has produced durable intermediate state (a saved draft, a committed database record), resume from that checkpoint rather than rerunning completed work. This applies only when the intermediate state is explicitly persisted and retrievable.

Default to discard-and-restart. Apply resume-from-checkpoint only when the cost of re-running completed work is measurably higher than the cost of resuming from partial state, and only when the intermediate state is verified as consistent.

---

## 4. Read-only vs. write risk tiers

The risk profile of the action, not the sophistication of the agent, determines the gate required.

| Action Type | Examples | Risk Tier | Gate Required | Restart Policy | Notes |
|---|---|---|---|---|---|
| Read and analyze | Read transcript, check knowledge base, classify a request | LOW | Sampled review | Discard + restart | Worst case: wrong answer caught in review |
| Draft artifact | Draft a BRD, summarize an ADR, generate a diagram | LOW | Sampled review | Discard + restart | Worst case: wrong draft returned to human |
| Update a field | Update Jira status, post a Confluence comment | MED | Explicit approve before write | Discard + restart + idempotency key | Confirm before any external write |
| Create a record | Create a Confluence page, open a Jira ticket | MED | Explicit approve before write | Discard + restart + idempotency key | Idempotency key prevents duplicate creation |
| Modify a requirement record | Edit a baselined requirement, update a compliance record | HIGH | Named human authority required | Idempotency key + documented rollback path | Cannot proceed without a named approver |
| Delete or archive | Remove a document, close a ticket set | HIGH | Named human authority required | Documented rollback only | No auto-rollback; rollback path must be documented before the step runs |

**Autonomy level is a property of the action, not the agent.** An agent trusted for LOW-tier drafting is not automatically trusted for MED-tier writes. Trust does not transfer across tiers.

---

## 5. Idempotency rule for write steps

Any step that writes to an external system needs an idempotency key. A retried write step without one produces a duplicate: two identical Confluence pages, two Jira tickets, two versions of the same requirement record.

The idempotency key must survive every retry and every reroute. Downstream systems use it to drop duplicate writes. The key is generated at the coordinator level and passed through every step that might touch the same external resource.

**Idempotency key per write step:**

| Write Step | Idempotency Key Source | Key Field Name | Drop-duplicate Logic |
|---|---|---|---|
| Create Confluence page | BR-identifier + draft version hash | `idem_key` | Check before create; return existing page ID if key matches |
| Update Jira status | Ticket ID + status transition + timestamp | `idem_key` | Skip if same transition already logged within 60s |
| Post review comment | Artifact ID + reviewer + timestamp bucket (1h) | `idem_key` | Check for duplicate comment before posting |

---

## 6. The annotation flywheel

Every rejected agent output is a new test case.

When a human reviewer rejects a step's output, three things happen:

1. The rejection reason is captured in a structured field (wrong content, wrong format, wrong source used, confidence mismatched)
2. The rejected output and its input are added to the evaluation set for that task type
3. Pattern analysis across rejections runs weekly to identify systemic failures: wrong routing, a step consistently struggling with a specific input type, a schema mismatch between steps

A pipeline without this loop is frozen at the quality of its first deployment. The evaluation set stops describing production within weeks.

The annotation flywheel is a named requirement, not a post-launch improvement. The data schema for rejection records must be defined before the pipeline ships.

**Rejection record schema:**

| Field | Type | Required |
|---|---|---|
| `rejection_id` | UUID | Yes |
| `step_name` | string | Yes |
| `task_type` | string | Yes |
| `input_hash` | string | Yes |
| `output_hash` | string | Yes |
| `rejection_reason` | enum: wrong_content / wrong_format / wrong_source / confidence_mismatch / other | Yes |
| `reviewer_id` | string | Yes |
| `timestamp` | ISO 8601 | Yes |
| `added_to_eval_set` | boolean | Yes |

---

## 7. Compounding error: reference numbers

Use these figures to anchor the case for validation gates in stakeholder conversations.

At 95% per-step success rate:
- 5 steps: 77% joint success
- 10 steps: 60% joint success
- 20 steps: 36% joint success

At 90% per-step success rate:
- 5 steps: 59% joint success
- 10 steps: 35% joint success
- 20 steps: 12% joint success

A validation gate between steps raises effective per-step reliability by catching errors before they propagate. A coding agent with a test feedback loop at each step achieves higher reliability than an open-ended task agent with the same base model, because the verifier shortens the effective chain that must succeed.

---

## 8. Self-check before the pipeline ships

1. Does every step have all six stop condition fields filled in the table?
2. Is the restart policy named per step: discard-and-restart or resume-from-checkpoint?
3. Is every write step classified in the risk tier table with a gate and an idempotency key?
4. Is the idempotency key schema defined for each write step before build?
5. Is the annotation flywheel rejection schema defined, with a named owner for weekly pattern analysis?
6. Is the rollback path documented for every HIGH-tier step before any agent is built?

---

## Related Artifacts

- [artifacts/post-47-automation-pipeline-map.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-47-automation-pipeline-map.md) - The pipeline shape this spec governs; five infrastructure layers and the coordinator-to-specialist handoff structure
- [artifacts/post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md) - The acceptance thresholds that define when a step's output is good enough to pass the validation gate
- [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) - The five-tier human checkpoint structure; HIGH-tier steps in this spec route to the blocked or kill-switch tier

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
