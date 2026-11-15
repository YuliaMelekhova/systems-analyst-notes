<!-- LinkedIn: -->

# Governance as Requirements Checklist

**Series:** Systems Analyst Notes  
**Post:** 74  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Turns eight common AI governance expectations into requirements a team can write down, own and test. Reach for it when a policy sentence such as "maintain an inventory" has no field, owner or test behind it.

---

## 1. How to read it

Each block starts with the policy phrase as it usually appears, then gives the same expectation as a requirement, a test, the evidence that proves it and the role that owns it. A requirement without a test is still a policy sentence, so the test is the part to keep.

The eight are a synthesis. They draw on three documents published between October 15 and November 4, 2026, and no single one of them lists these eight in this form. None of the three creates a binding rule, so check each row against the regulator that applies to you.

| Source | Date | Status |
|---|---|---|
| Financial Stability Board, Sound Practices for Responsible Adoption of Artificial Intelligence | October 15, 2026 | Nonbinding, proportionate to size and risk |
| OCC Bulletin 2026-54, Super Intelligence: Supervisory Framework | November 4, 2026 | Examiner resource, sets no expectations for banks |
| FCA, AI in financial services: good practice and areas for improvement, with a speech by Jessica Rusu | October 19, 2026 | Guidance examples, the speech is a drafted text |

---

## 2. The eight requirements

### 1. Policy phrase: "Maintain an AI inventory"

* **Requirement:** Every AI use, every agent and every AI feature inside vendor software has one row in a single register. The row holds the use case, the owner, the provider, the permissions, the status and the date of the last review.
* **Test:** Pick any agent running in production and find its row, with a named owner, in under five minutes. Then pick one vendor tool and ask whether it contains AI that is missing from the register.
* **Evidence:** The register, with its change history.
* **Owner:** The risk or platform lead who maintains the register. Each row names its own use case owner.

### 2. Policy phrase: "Define the intended use"

* **Requirement:** Before deployment and after any material change, a purpose statement records what the system is designed to do, what it is not designed to do, who or what may invoke it, which data and systems it may reach, and when a human must review or suspend it.
* **Test:** Take ten logged actions at random and classify each as inside or outside the purpose without asking the builder.
* **Evidence:** A versioned purpose statement linked from the register row.
* **Owner:** The use case owner.

### 3. Policy phrase: "Control access to data"

* **Requirement:** Permissions to data and tools are enforced by code outside the model. The agent's goals, its permissions and the data it can reach are kept apart, so changing one does not quietly change another.
* **Test:** Ask the system to read a record or call a tool outside its scope. The call is refused and the refusal appears in the log.
* **Evidence:** The permission set, the tool allowlist and one logged refusal.
* **Owner:** The technical owner of the system.

### 4. Policy phrase: "Keep an audit trail"

* **Requirement:** For each consequential output, one record holds the input, the model and configuration version, the sources retrieved, the tool calls, the reviewer's action and rationale, and the outcome. Records are protected from silent edits.
* **Test:** Choose one decision from last month and rebuild it from a single query.
* **Evidence:** The decision record and the write-protection settings on the store that holds it.
* **Owner:** The platform owner, with compliance as the reader of the result.

### 5. Policy phrase: "Ensure human oversight"

* **Requirement:** Named steps pause for a human unconditionally. The specification states what the reviewer sees, how many items one person reviews per shift, and how an override is recorded with a reason.
* **Test:** Pull the approval log for one reviewer over a month and read the approval rate and the time per decision. A rate near 100% means the step guards nothing or is not being read.
* **Evidence:** The checkpoint specification and the reviewer log.
* **Owner:** The business owner of the process the checkpoint sits in.

### 6. Policy phrase: "Set performance thresholds"

* **Requirement:** Each task type has a success metric, a number below which it does not ship, and a named owner for the decision when a result lands under that number. The threshold is written before deployment and tied to a fixed evaluation set and a pinned model version.
* **Test:** Ask for the threshold of one task type and the date it was written. A date after the first demo means the number describes a result and sets no bar.
* **Evidence:** The acceptance criteria table and the evaluation set version.
* **Owner:** The use case owner.

### 7. Policy phrase: "Be able to stop the system"

* **Requirement:** Each agent has a halt procedure. It stops sub-agents as well as the parent, and the logs, the queue state and the audit trail stay readable afterward.
* **Test:** Halt a parent agent in a test environment and confirm every sub-agent stops. Repeat on a schedule, because a halt that was built and never run is an assumption.
* **Evidence:** A dated test report and the written halt procedure.
* **Owner:** The technical owner, with the incident lead.

### 8. Policy phrase: "Manage third-party AI"

* **Requirement:** Vendor contracts cover notice of material changes that affect AI behavior, data retention and processing location, audit rights, and responsibility for version updates. A vendor change triggers a retest of the affected use cases.
* **Test:** Pick one vendor product and find the clause that gives notice before a model change. Then find the record of the last retest after a version update.
* **Evidence:** The contract clauses and the retest record.
* **Owner:** The procurement owner, with the technical owner for the retest.

---

## 3. Using it

**Step 1: Copy the blocks into your own page.** Replace each owner role with a name. A role with no name behind it is the first gap.

**Step 2: Run each test once.** Record the date and the result in the register row, including the tests that fail.

**Step 3: Turn every failed test into a backlog item.** Give it an owner and a date, the same way any other requirement is handled.

**Step 4: Re-run the tests when something underneath changes.** A new model version, a new tool, a changed permission set or a vendor update each count.

## 4. What stays policy

How much risk a board is willing to accept is a judgment, and no test settles it. The checklist starts below that line, with everything a team can write as a field, an owner and a test.

---

## Related Artifacts

* [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) - The checkpoint tiers that requirement 5 points at, including the kill switch condition and re-enable path
* [artifacts/post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md) - The parameters behind the purpose statement in requirement 2
* [artifacts/post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md) - The shipping threshold, review policy and owner per task type behind requirement 6
* [artifacts/post-72-requirement-ownership-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-72-requirement-ownership-template.md) - One accountable owner per requirement and per agent, which the owner column here relies on

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
