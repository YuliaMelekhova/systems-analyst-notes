<!--
Post: 19
Title: Mapping the Unhappy Path Before You Design the Happy One
Phase: 3 - Building the Foundation
LinkedIn: [link once published]
-->

# Unhappy Path Mapping Framework

**Series:** Systems Analyst Notes  
**Post:** 19  
**Phase:** 3 Building the Foundation  
**Author:** Yulia Melekhova  
**Published:** 2026  

---

## Purpose

The happy path is what you design first. The unhappy paths are what you must document before the happy path is finalized. A requirement that maps only the happy path describes a system that works in testing. Unhappy paths are where the system actually fails - and in regulated environments, where the most expensive failures happen.

---

## The Core Principle

Map unhappy paths before writing the requirement - not as a post-processing step.

Every unhappy path has four components:

| Component | Description |
|-----------|-------------|
| **Trigger** | The condition that causes the happy path to fail |
| **System response** | What the system does when the trigger fires |
| **Regulatory implication** | Which obligation, if any, applies to this failure mode |
| **Resolution path** | What must happen before the flow can continue or close |

---

## Unhappy Path Categories

### 1. Data Failure Paths

Occur when input data is missing, malformed, or below the quality threshold the downstream system requires.

**Template:**

| Field | Content |
|-------|---------|
| Trigger | `[field name]` is null / empty / fails validation |
| System response | Block / reject / hold / route to exception queue |
| Regulatory implication | Which compliance gate depends on this field |
| Resolution path | Manual correction / automated enrichment / rejection with reason code |

**Fintech example - ISO 20022 structured address:**  
Trigger: `TwnNm` or `Ctry` absent from pacs.008 party fields.  
System response: SWIFT CBPR+ rejects message.  
Regulatory implication: Non-compliance with November 14, 2026 structured address mandate.  
Resolution path: Address enrichment from CRM/ERP before message generation. Value-date, not submission date, determines compliance window.

---

### 2. Threshold Failure Paths

Occur when a value crosses a regulatory or business threshold that changes the required behavior.

**Template:**

| Field | Content |
|-------|---------|
| Trigger | Amount / count / frequency exceeds `[threshold]` |
| Regulatory regime | Which law or regulation defines the threshold |
| Obligation triggered | What the system must do once threshold is crossed |
| Cross-jurisdiction check | Does the same transaction trigger a different threshold in another jurisdiction? |

**Fintech example - FATF Travel Rule:**  
Trigger: Transaction amount exceeds $2,500 (US obligation).  
Regulatory regime: FATF Travel Rule, FinCEN implementation.  
Obligation triggered: Originator and beneficiary information must travel with the payment.  
Cross-jurisdiction check: Same transaction may simultaneously trigger EU Travel Rule obligations at a different threshold. Both apply.

---

### 3. Verification Failure Paths

Occur when a counterparty, identity, or instrument fails a compliance check.

**Template:**

| Field | Content |
|-------|---------|
| Trigger | Watchlist / KYC / sanctions check returns non-passing result |
| Failure types | Hard block / soft hold / manual review required |
| Hold behavior | Duration, notification, escalation path |
| Release condition | What evidence or approval releases the hold |

**Fintech example - sanctions screening:**  
Trigger: Beneficiary name matches OFAC SDN list.  
Failure type: Hard block - payment cannot proceed.  
Hold behavior: Automated hold initiated; compliance team notified within [X] minutes; payment placed in restricted queue.  
Release condition: Compliance officer manual review with documented rationale. Audit log updated.

---

### 4. Regulatory Conflict Paths

The most expensive category. Occur when two regulatory regimes impose conflicting obligations on the same transaction.

These do not resolve through technical design alone. They require a documented decision about which obligation takes precedence, or how both can be satisfied simultaneously.

**Template:**

| Field | Content |
|-------|---------|
| Conflict | Regime A requires `[action]`. Regime B prohibits `[same action]`. |
| Jurisdictions involved | Which countries / regulators are in conflict |
| Documented decision | How the product owner and legal team resolved the conflict |
| System behavior | What the system does when this conflict is triggered |
| Audit record | What is logged to demonstrate compliance with the chosen resolution |

**Fintech example - GDPR vs. FATF Travel Rule:**  
Conflict: GDPR restricts transmission of personal data beyond the EU. FATF Travel Rule mandates transmission of originator and beneficiary data with the payment.  
Jurisdictions: EU (GDPR) vs. FATF member states (Travel Rule).  
Documented decision: [Requires explicit legal sign-off - do not default this to engineering.]  
System behavior: Payment flagged for manual compliance review if both obligations apply simultaneously.  
Audit record: Compliance decision, reviewer identity, timestamp, rationale.

---

## Mapping Process

1. Write the happy path in full.
2. At each step of the happy path, ask: "What can fail here?"
3. For each failure: classify it (data / threshold / verification / regulatory conflict).
4. Fill in all four components of the unhappy path template.
5. Identify any two failure paths that interact (e.g., a threshold crossing that also triggers a sanctions check).
6. Flag any unhappy path that requires a legal or compliance decision that has not yet been made. Do not baseline the requirement until those decisions are documented.

---

## Compliance Intersection Checklist

Before finalizing any cross-border payment requirement, check each of the following:

- [ ] Travel Rule: does the transaction cross the threshold in any involved jurisdiction?
- [ ] Sanctions screening: is there a specified response for each possible result (pass / hold / block)?
- [ ] ISO 20022 structured address: are all required fields (`TwnNm`, `Ctry` minimum) present in every upstream data source?
- [ ] GDPR / data transfer: does the payment require transmitting personal data to a jurisdiction with different data protection rules?
- [ ] AML monitoring: which transaction patterns trigger a Suspicious Activity Report, and what does the system do while the report is pending?
- [ ] Currency corridor: do the unhappy paths account for jurisdiction-specific rules (CHAPS, SEPA, CBPR+) for each corridor named in the requirement?

---

## Related Artifacts

* [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) - Step 4 of the discovery framework covers unhappy path discovery
* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - Prerequisites before writing a requirement
* [knowledge-packs/iso-20022-cbpr-plus.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/iso-20022-cbpr-plus.md) - The field rules behind the structured address line in the compliance checklist
* [stride-threat-modeling/payment-initiation-stride.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/stride-threat-modeling/payment-initiation-stride.md) - Every threat there produces an unhappy path that needs a specified response
* [templates-quality-rules/requirement-antipatterns.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/requirement-antipatterns.md) - Success-only specification, which is this framework's absence seen from the review side

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova

