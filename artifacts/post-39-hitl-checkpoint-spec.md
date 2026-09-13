<!-- LinkedIn: -->

# Human-in-the-Loop Checkpoint and Kill Switch Specification

**Series:** Systems Analyst Notes  
**Post:** 39  
**Phase:** 5 Bringing AI Into the Workflow  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Defines five checkpoint tiers for an AI agent, the control that enforces each one outside the model, and a separate kill switch specification for system-wide shutdown. Fill in the fintech examples, the named owners, and the two thresholds once per deployment.

---

## 1. Scope

This spec covers checkpoint placement for one AI agent or one agent pipeline making consequential decisions in a fintech workflow: drafting, recommending, updating records, or initiating a transaction. It does not cover general software approval workflows that involve no model.

Two values get set once per deployment and referenced throughout.

| Value | Written as | Set by |
|---|---|---|
| Fraud spike threshold that fires the kill switch | `[FRAUD_THRESHOLD]` | Risk team with the agent owner |
| KPI drop threshold that fires the kill switch | `[KPI_THRESHOLD]` | Business owner with the agent owner |

---

## 2. Design principle: the orchestrator decides, not the model

A model is non-deterministic. Asking it to decide, mid-task, whether its own output needs human review puts the decision inside the component the review exists to check. The pause points are fixed at build time, by the workflow definition, not discovered at runtime by the agent.

Two requirements follow from this, and both must be named before build:

Which steps trigger a mandatory pause regardless of the model's reported confidence.
Which signals allow the agent to auto-progress without a pause.

"The agent pauses when it's unsure" is not a checkpoint spec. "The agent pauses after step 3 and step 7, unconditionally, and a human must approve before the workflow continues" is a checkpoint spec.

---

## 3. The five checkpoint tiers

Friction scales with risk, not with uniform caution. A single approve-or-reject gate treats a drafted note the same as a wire transfer, and that mismatch is a defect in the spec, not a simplification of it.

| Tier | Definition | Fintech example | Enforcing control | Gate type |
|---|---|---|---|---|
| Auto-proceed | Low risk, reversible, no external effect | Drafting an internal summary note | Output guardrail screens content before it is shown | Soft |
| Lightweight confirm | A recommendation a human can scan and confirm in seconds | A pricing exception recommendation with citations attached | Confidence threshold gate plus a citation check | Soft |
| Explicit approval | Touches a shared record or hands work to another team | Updating a compliance record, drafting a cross-team task | A visible action proposal must be signed off before the tool call executes | Hard |
| Blocked | Touches money, compliance status, or an external party | Initiating a payment, changing a credit limit | The tool allowlist carries no credential for this action without a prior approval | Hard |
| Kill switch | System-level shutdown triggered by a defined signal, not a per-action review | `[FRAUD_THRESHOLD]` crossed, `[KPI_THRESHOLD]` crossed, manual override from the risk team | The runtime guardrail halts the agent loop entirely and routes to manual takeover | Hard |

Gate type matters beyond labeling. A hard gate blocks execution pending approval. A soft gate lets execution proceed and logs the approval after. Most deployments record neither field, and a queryable record of which type applied to which decision is what a regulator asks for during review. Declare the gate type per checkpoint. Do not assume it.

---

## 4. Kill switch specification

The kill switch is not a sixth degree of the same caution as Blocked. Blocked stops one action and waits for a decision on that action. The kill switch stops the entire agent loop.

**Condition.** The specific signal that fires it: `[FRAUD_THRESHOLD]` crossed on transaction velocity, `[KPI_THRESHOLD]` crossed on a monitored business metric, or a manual override entered by a named risk team role. State the signal as a measurable threshold, not a judgment call a person makes in the moment.

**Effect.** What happens the instant it fires: the agent loop halts, every in-flight action is logged with its last known state, an incident record opens automatically, and control routes to manual takeover. No in-flight write completes after the signal fires. A write already committed before the signal is left as is and handled through the incident process, not silently rolled back.

**Re-enable path.** Who can restart the loop, and under what condition: a named role, not "whoever notices first," reviews the incident record and signs off before the agent resumes. The re-enable action itself is logged with the same reviewer identity and timestamp fields required in section 6.

---

## 5. Reviewer requirements

A checkpoint with an untrained reviewer is not a lighter version of a real control. It looks present on an audit and is not present in practice, because the presence of a person is not the control. The person's judgment is, and judgment degrades under volume and fatigue the same way any other system component does.

Four skills are required before a person is assigned to any tier above Auto-proceed:

Framing a better prompt when the agent's first output does not answer the question.
Supplying the right context the agent was missing.
Spotting an inaccuracy in the output that reads as fluent and correct.
Knowing when the decision needs to escalate past them entirely.

A reviewer who cannot articulate what evidence would change their answer has not been trained to review. They have been trained to click.

---

## 6. Audit record fields per checkpoint decision

Every checkpoint decision, at any tier above Auto-proceed, writes the following fields to a record the agent itself did not generate:

Reviewer identity, review timestamp, review action taken (approve, override, or escalate), the rationale for that action, any correction applied to the agent's output, the outcome after the decision, and the gate type (hard or soft) that applied.

Sensitive values referenced in the review (compensation figures, account numbers, health information) are logged as accessed, not logged in value. The field-level distinction is deliberate: a log stating that a field was reviewed satisfies the audit requirement, and a log storing the field's contents creates a second compliance exposure while solving the first.

---

## 7. Review gate

Five checks before this spec is considered ready for a specific agent deployment.

1. Does every checkpoint tier above Auto-proceed have a named enforcing control that sits outside the model, not a system instruction asking the model to behave?
2. Is the kill switch condition written as a measurable threshold, with `[FRAUD_THRESHOLD]` and `[KPI_THRESHOLD]` filled in rather than left as placeholders?
3. Does every reviewer assigned to a tier meet the four-skill bar in section 5, with a named training record?
4. Is the gate type, hard or soft, declared per checkpoint rather than assumed?
5. Is the re-enable path named to a specific role, with the sign-off logged under the same fields as every other checkpoint decision?

A spec that fails check 2 is the one that ships, passes review, and cannot actually stop anything when the signal it was built for finally fires.

---

## Related Artifacts

* [artifacts/post-25-sequence-diagram.mmd](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.mmd) - Shows the live cross-service call a checkpoint would sit inside, before the tier is assigned
* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - Where the kill switch trigger decision gets recorded once the two thresholds are set

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
