<!-- LinkedIn: -->

# Governance as Requirements Checklist

**Series:** Systems Analyst Notes  
**Post:** 74  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Translates eight common AI governance control objectives into example requirements, tests, evidence, and ownership. Use it to identify implementation gaps and prepare backlog items for a specific AI use case.

---

## 1. How to read it

Each block gives an example requirement, checks that can reveal implementation gaps, evidence to retain, and an accountable owner role. Tests provide evidence of control behavior within their stated scope; a passing sample does not prove complete coverage or compliance.

The eight areas are an author-created synthesis of the publications below. No single source prescribes this checklist. The tests, sample sizes, response times, and implementation choices are illustrative internal controls, not regulator-prescribed acceptance criteria. Before using them, document the system boundary, risk tier, applicable obligations, approved thresholds, and any justified exclusions. Replace illustrative targets with approved values or rule references.

The FSB practices are nonbinding. The OCC framework is an examiner resource that establishes no new supervisory expectations for banks. The FCA review shares supervisory observations and reminders about existing obligations; its AI findings include weaknesses identified by banks' internal audit functions. Those findings do not establish how prevalent the weaknesses are across the industry.

| Source | Date | Status |
|---|---|---|
| Financial Stability Board, [Sound Practices for Responsible Adoption of Artificial Intelligence (AI): Final report](https://www.fsb.org/2026/10/sound-practices-for-responsible-adoption-of-artificial-intelligence-ai-final-report/) | October 15, 2026 | Nonbinding practices to apply proportionately to the institution and use case |
| OCC Bulletin 2026-54, [Super Intelligence: Supervisory Framework](https://www.occ.gov/news-issuances/bulletins/2026/bulletin-2026-54.html) | November 4, 2026 | Examiner resource; establishes no new supervisory expectations or enforceable standards for banks |
| FCA, [Wholesale banks supervision - Insights 3 (Autumn 2026)](https://www.fca.org.uk/publications/multi-firm-reviews/wholesale-banks-supervision-insights-3-autumn-2026), multi-firm review | November 2, 2026 | Supervisory observations, including internal audit findings; distinct from the FCA and Bank of England AI survey |

Requirement 7 draws on the FCA's observations about kill switch training, testing, maintenance, and authorized operators. The proposed sub-agent and queue checks extend those observations into an illustrative technical test.
---

## 2. The eight requirements

### 1. Policy phrase: "Maintain an AI inventory"

* **Requirement:** Each in-scope AI use case has a uniquely identified entry in an authoritative inventory, including AI embedded in vendor products. Link agents, models, and shared components to their use cases without duplicating ownership. Record the accountable owner, provider, purpose, permissions or permission references, risk tier, lifecycle status, and last review date. Reconcile the inventory with deployment and procurement records on an approved schedule.
* **Test:** Select a production agent independently from deployment records and locate its current inventory entry and named owner within the approved retrieval target, for example, five minutes. Compare its provider, status, and permissions with the deployed configuration. Sample a vendor product and check available disclosures for unregistered AI features. Record the sample scope and discrepancies; one successful lookup does not establish inventory completeness.
* **Evidence:** Inventory entries, change history, reconciliation results, and the approved retrieval target.
* **Owner:** The designated inventory owner, supported by a named accountable owner for each use case.

### 2. Policy phrase: "Define the intended use"

* **Requirement:** Before deployment, approve a versioned purpose statement defining permitted and prohibited actions, authorized callers, accessible data and systems, and triggers for human review or suspension. Reassess it before releasing a material change. Define how undocumented or ambiguous actions are escalated.
* **Test:** Sample logged actions against the purpose statement effective at the time of execution. Ten actions can be an initial sample, with the final sampling approach based on risk. Include boundary cases and prohibited actions in controlled tests. Confirm that actions can be classified without relying on undocumented knowledge and that prohibited actions are blocked or escalated as specified.
* **Evidence:** Approved purpose statement, version history, linked inventory entry, and classification and boundary-test results.
* **Owner:** The use case owner.

### 3. Policy phrase: "Control access to data"

* **Requirement:** Enforce data and tool permissions at trusted authorization boundaries outside the model, using least privilege. Changes to prompts or goals must not independently expand access. Define caller and agent identities, resource and tenant scope, credential handling, permission revocation, and denial logging.
* **Test:** In a controlled environment, attempt an unauthorized record read and tool action through the actual authorization boundary. Include another tenant's resource, a revoked permission, and a prompt that asks the agent to bypass restrictions. Confirm denial before data disclosure or side effects, with a correlated denial event. Verify an authorized operation still succeeds. A model's verbal refusal alone is insufficient evidence.
* **Evidence:** Versioned access policy, identity and tool configuration, test results, and denial logs that exclude secrets.
* **Owner:** The technical owner of the system, with the access-control owner.

### 4. Policy phrase: "Keep an audit trail"

* **Requirement:** Define which outputs and actions are consequential. For each, retain a correlated record of the relevant input or permitted reference, available model identifier, configuration version, retrieved source references, tool requests and results, output, resulting action, and any required human decision and rationale. Explicitly identify unavailable provider metadata. Apply approved retention, minimization, access, and tamper-protection controls.
* **Test:** Select a retained decision and reconstruct its recorded sequence using correlation identifiers. Verify the applicable configuration, evidence references, outcome, and required review. Check retrieval permissions and detection or prevention of unauthorized alteration. Reconstructing the record does not require identical model output on rerun or access to hidden model reasoning.
* **Evidence:** Correlated decision records, retention and access policies, integrity controls, and reconstruction-test results.
* **Owner:** The platform owner, with compliance and privacy stakeholders defining applicable evidence requirements.

### 5. Policy phrase: "Ensure human oversight"

* **Requirement:** Define which actions require approval before execution and which allow monitoring with intervention. At mandatory approval checkpoints, execution remains blocked until an authorized reviewer approves. Specify the evidence presented, reviewer authority and capacity, timeout and unavailability behavior, and logging of approvals, rejections, and overrides. Define any exception path explicitly.
* **Test:** Confirm that a gated action cannot execute without valid approval, including when the reviewer is unavailable or the request times out. Present a known incorrect output in a controlled review exercise and check detection and escalation. Review approval rates and decision times alongside case complexity and sampled decision quality. A near-100% approval rate warrants investigation but does not by itself prove ineffective oversight.
* **Evidence:** Checkpoint specification, authority matrix, review and override logs, and controlled review-test results.
* **Owner:** The business owner of the process, with a designated owner for reviewer training and capacity.

### 6. Policy phrase: "Set performance thresholds"

* **Requirement:** For each task type, approve relevant quality, safety, and operational metrics, pass/fail thresholds, and evaluation methods before the acceptance evaluation. Specify whether higher or lower values are better. Version the evaluation data, model identifier, prompts, configuration, and tools. Define release-blocking criteria, production escalation thresholds, and the owner of remediation or any permitted exception.
* **Test:** Compare approval timestamps with the acceptance evaluation and verify that thresholds were not adjusted solely to pass an observed result. Check the specified model and configuration against the evaluation record and rerun the approved evaluation, including relevant failure and boundary cases. For variable outputs, use a predefined repetition and aggregation method. Confirm that a failed release-blocking criterion prevents release unless an explicitly permitted exception is approved and recorded. A threshold set after an exploratory demo can still be valid.
* **Evidence:** Approved criteria, evaluation protocol and dataset versions, configuration identifiers, results, and any exception record.
* **Owner:** The use case owner, with the designated evaluation owner.

### 7. Policy phrase: "Be able to stop the system"

* **Requirement:** Define a risk-appropriate halt procedure, a current list of authorized operators, training, and an approved maximum time to reach the specified safe state. Define treatment of the parent, sub-agents, queued work, in-flight calls, retries, and scheduled restarts. Prevent further unauthorized actions and preserve relevant logs and queue evidence. Identify actions that cannot be canceled and define containment or remediation. Specify controlled restart authorization. Retest on an approved schedule and after changes that can affect halt behavior.
* **Test:** In a controlled environment, have a trained authorized operator invoke the procedure using the approved runbook. Verify the safe state within the approved time, including child agents, queued tasks, in-flight work, and retry behavior. Confirm that unauthorized operators cannot invoke privileged controls, evidence remains accessible to authorized staff, and restart requires the specified authorization. Document any irreversible action and its handling.
* **Evidence:** Versioned halt and restart procedures, operator authorization and training records, timed test results, and preserved execution evidence.
* **Owner:** The technical owner, with the incident lead responsible for operational readiness.

### 8. Policy phrase: "Manage third-party AI"

* **Requirement:** For each relevant provider, document AI dependencies and agreed terms for material-change notification, permitted data use, retention, processing location, assurance or audit access, incident handling, and version-update responsibility. Require advance notice where needed for the use case. If contractual or technical visibility is limited, document compensating controls and an explicit risk decision. Assess changes and retest affected use cases before release where controlled, or under an approved response plan for provider-controlled changes.
* **Test:** Select a vendor product and compare its actual terms and controls with the use case's approved requirements. Trace a material change from notification or detection through impact assessment, testing, and the release or continuation decision. If no change has occurred, run a simulated notification scenario. Record unavailable notice, version pinning, or audit rights as gaps requiring mitigation or an authorized risk decision.
* **Evidence:** Vendor assessment, relevant contract clauses, change notifications or detection records, impact assessments, test results, and risk decisions.
* **Owner:** The procurement or vendor relationship owner, with the technical owner responsible for impact assessment and retesting.

---

## 3. Using it

**Step 1: Copy the blocks into your own page.** Define the system boundary, applicable obligations, and risk tier. Adapt each requirement and test, approve the thresholds, and map each accountable role to a named person or maintained ownership record. Document justified exclusions and unresolved gaps.

**Step 2: Run each test once.** Use a controlled environment for tests that could expose data or trigger side effects. Record the tested configuration, sample, expected and observed results, date, tester, and evidence. Distinguish Pass, Fail, Not Tested, and Not Applicable; require a rationale for Not Applicable. An initial run establishes a baseline, not continuing assurance.

**Step 3: Turn every failed test into a backlog item.** Record the affected requirement, risk, accountable owner, target date, remediation, and retest criteria. Escalate urgent failures through incident or release-control procedures rather than waiting for routine backlog prioritization. Record any authorized, time-limited risk acceptance separately from a passing result.

**Step 4: Re-run the tests when something underneath changes.** Assess changes to models, prompts, tools, permissions, data sources, vendors, and process design. Rerun affected checks and relevant regression tests, and follow the approved periodic review schedule. Keep the evidence linked to the configuration actually tested.

## 4. What stays policy

Risk appetite, accountability, and acceptable trade-offs require authorized judgment within applicable legal and regulatory constraints. Tests can show whether a control behaves as specified; they cannot decide whether the chosen level of risk is acceptable. Record the rationale, decision authority, residual risk, and review triggers. Passing this checklist does not establish regulatory compliance or remove the need for independent challenge.

---

## Related Artifacts

* [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) - Companion checkpoint specification for human oversight and intervention
* [artifacts/post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md) - Companion instruction standard for documenting agent scope and constraints
* [artifacts/post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md) - Companion acceptance criteria for task-level evaluation and release decisions
* [artifacts/post-72-requirement-ownership-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-72-requirement-ownership-template.md) - Companion template for recording accountable ownership

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
