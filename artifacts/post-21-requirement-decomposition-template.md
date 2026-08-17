<!-- LinkedIn:  --> https://www.linkedin.com/posts/yuliamelekhova_systemsanalysis-requirementsengineering-microservices-share-7494720407485329410-8-R0/?utm_source=social_share_send&utm_medium=member_desktop_web&rcm=ACoAABW2QzcBN4fI21bG0ls7u2nHq-ooXTFxjEU

# Multi-Service Requirement Decomposition Template

**Series:** Systems Analyst Notes  
**Post:** 21  
**Phase:** 4 APIs as Products  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

Breaks a single requirement into the services it actually touches, naming an owner and a contract per service before the requirement goes to baseline. Reach for it whenever a requirement crosses more than one service boundary, which in a microservice platform is most of them.

---

## How to use this file

Copy the six sections below into the requirement itself, not into a separate document. A decomposition stored apart from the requirement goes stale the first time either one is edited.

Fill the sections in order. Section 5 cannot be completed honestly until sections 1 through 4 are done, which is the point of the ordering.

Anything unknown is written as `UNKNOWN` with a named person against it. A blank cell reads as "nothing here." `UNKNOWN` reads as "someone still has to answer this," and those are different states.

---

## Section 1: Requirement header

| Field | Value |
|---|---|
| Requirement ID | |
| Title | |
| Triage tier | Critical / Important / Nice-to-have / Not now |
| Business goal, one sentence | |
| Requested by | |
| Accountable owner | |
| Target baseline date | |

The accountable owner is one named person, not a team. If two names go in this cell, the requirement has not been decomposed yet.

---

## Section 2: Service participation

One row per service the requirement touches. A service that only reads data still gets a row, because a schema change breaks readers before it breaks writers.

| Service | Role in this requirement | Owner | Contract touched | Change type | Sign-off needed |
|---|---|---|---|---|---|
| | Producer / Consumer / Router / Store / Gate | | | New / Breaking / Non-breaking / None | Yes / No |

Definitions for `Role`:

* **Producer** emits the message or event this requirement changes.
* **Consumer** reads it and behaves differently as a result.
* **Router** decides where it goes without changing its content.
* **Store** persists it, which makes it the service that carries any migration cost.
* **Gate** can block the flow, usually a compliance, fraud or authorization check.

`Change type` is answered against the contract, not against the code. A field added as optional is non-breaking. The same field added as mandatory is breaking, whatever the implementation looks like.

---

## Section 3: Message and stage inventory

For a payment requirement, the stage sequence is the spine of the decomposition. Each stage gets its message type, its owner and its validation rules named.

| Stage | Message type | Owning service | Schema version | Validation rules that apply | Changes under this requirement |
|---|---|---|---|---|---|
| Initiation | | | | | |
| Validation | | | | | |
| Routing | | | | | |
| Clearing | | | | | |
| Settlement | | | | | |
| Status and returns | | | | | |
| Reconciliation and reporting | | | | | |
| Archiving | | | | | |

A requirement that changes one row here and leaves the rest empty is either genuinely narrow or incompletely analyzed. The table is what forces that question to be asked out loud.

---

## Section 4: Corridor and standard mapping

Cross-border requirements behave differently per corridor, so the corridor is a dimension of the requirement rather than a footnote to it.

| Corridor | Message standard | Compliance gates between stages | Acceptable rails | Ticket size band |
|---|---|---|---|---|
| | ISO 20022 MX / ISO 8583 / local scheme | Sanctions / AML / KYC / Travel Rule | Correspondent / SWIFT / stablecoin / local rail | |

Where a rail is acceptable only below a threshold, the threshold goes in the last column as a number. "Small payments" is not a threshold.

---

## Section 5: Blast radius

For each service in section 2, answer what happens when this requirement is deployed and something is wrong.

| Service | Upstream producers | Downstream consumers | Failure mode if this change is wrong | Detected by | Rollback path |
|---|---|---|---|---|---|
| | | | | | |

`Detected by` names a monitor, an alert or a report. "The team would notice" is not a detection mechanism.

This section is what an automated actor reads before it is allowed to act against a service. An agent with access to a service and no view of its dependencies is the same risk as an analyst writing a requirement against one service without knowing who consumes it. The two failures have produced the same incident more than once.

---

## Section 6: Completeness check

Run before baseline. Any `no` sends the requirement back rather than forward.

1. Does every service in section 2 have a named owner who has seen this requirement?
2. Does every stage in section 3 that carries a change have a schema version against it?
3. Does every corridor in section 4 name its compliance gates, including the ones that do not change?
4. Does every row in section 5 have a detection mechanism and a rollback path?
5. Does any cell still read `UNKNOWN` without a name attached to it?
6. Would a reader who has never seen this platform be able to list the affected services from this document alone?

---

## Worked example: raising the settlement retry limit

A one-line request, decomposed.

**Request as received:** "Raise the retry limit on failed settlement from 3 to 5 for the Mexico corridor."

**Section 2, service participation:**

| Service | Role | Owner | Contract touched | Change type | Sign-off needed |
|---|---|---|---|---|---|
| settlement-orchestrator | Producer | Backend lead | `settlement.retry.policy` config schema | Non-breaking | Yes |
| corridor-router | Router | Backend lead | none | None | No |
| compliance-gate | Gate | Compliance lead | none | None | Yes |
| reconciliation-service | Consumer | Data lead | `camt.053` daily report | Non-breaking | Yes |
| notification-service | Consumer | Product owner | customer status copy | Non-breaking | No |

**What the decomposition surfaced:** the reconciliation report groups retries by attempt number and has a fixed set of three columns. Five attempts break the report layout, which nobody would have found until the first month-end after deployment. The request touched one config value and four services.

**Blast radius entry that mattered:**

| Service | Failure mode if wrong | Detected by | Rollback path |
|---|---|---|---|
| reconciliation-service | Attempts 4 and 5 dropped silently from the daily report, understating failed settlement volume | Daily volume reconciliation alert, threshold 2% variance | Revert config to 3, reprocess affected report days |

---

## Related Artifacts

* [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) - Step 2 of discovery produces the context that this template decomposes
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Section 5 blast radius feeds directly into unhappy path mapping per service
* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - Every contract named in section 2 gets specified here before build
* [artifacts/post-16-context-diagram.mmd](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.mmd) - Draw the boundary first, then decompose what sits inside it

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
