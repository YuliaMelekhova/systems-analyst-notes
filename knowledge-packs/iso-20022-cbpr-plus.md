# ISO 20022 CBPR+ Structured Address Knowledge Pack

Series: Systems Analyst Notes
Branch: Knowledge Packs
Author: Yulia Melekhova
Published: 2026

## Purpose

A reference on what the November 14, 2026 CBPR+ address requirement changes in a payment system, written for the person who has to specify the data model and the API contract. Reach for it when scoping a payment initiation flow, reviewing an existing integration, or deciding how much of the address structure to build now.

---

## What CBPR+ Is

Cross-Border Payments and Reporting Plus is the Swift market practice layer sitting on top of ISO 20022. ISO 20022 defines the message schemas. CBPR+ defines how the community agreed to use them: which elements are mandatory, which are optional, what validation the network applies. Two banks can both be ISO 20022 compliant and still fail to exchange a payment if one of them ignores CBPR+ usage guidelines.

The distinction matters for a spec. Pointing at "ISO 20022" in a requirements document is not precise enough to build against. The binding constraint is the CBPR+ Usage Guideline for the specific Standards Release, and it changes annually.

Two dates already passed and shape the current state:

* November 22, 2025: the MT and ISO 20022 coexistence period for CBPR+ cross-border payments ended. ISO 20022 became the required format for in-scope Swift activity.
* November 2025: the hybrid postal address option entered the SR 2025 Usage Guidelines, opening a one-year window to move off unstructured addresses.
* February 20, 2026: the final SR 2026 Usage Guidelines, including the formal validation that retires unstructured addresses, became available.
* November 14, 2026: the validation takes effect.

---

## What Changes on November 14, 2026

Two separate requirements land on the same date. Teams that prepared for one and missed the other will be non-compliant in a message family they never looked at.

**Requirement one: postal addresses.** Fully unstructured postal addresses are no longer accepted in CBPR+ payment messages. Where address information is provided, it must be fully structured or hybrid. Non-compliant messages are rejected on the network. Swift has stated there is no contingency measure.

**Requirement two: enquiry and investigation messages.** Financial institutions must be able to receive camt.110 and camt.111 in MX format from the same date. This is a different message family from pacs.008 and friends, and it is frequently owned by a different team internally.

### Scope of the address requirement

Town Name and Country must be present in designated fields, at minimum, for all agents and parties in CBPR+ payment messages. The requirement applies to corporate, securities, trade, FX and funds payments, not only to the obvious retail cross-border case.

Excluded message identifiers: admi.024, camt.025, camt.052, camt.053, camt.054, camt.060.

For agents specifically, supplying BIC only remains valid as an alternative to name and address. That exception applies to agents, not to debtors and creditors.

The requirement reaches domestic payments that carry a cross-border leg, and it reaches future-value-dated payments. A payment initiated before the deadline with a value date on or after November 14, 2026 needs a compliant address.

---

## The Three Address Formats

| Format | What it contains | Status after November 14, 2026 |
|---|---|---|
| Unstructured | Free text address lines, `AdrLine` only | Rejected |
| Hybrid | Structured Town Name and Country, remaining detail in `AdrLine` | Accepted, minimum viable compliance |
| Fully structured | Every component in its own tag, up to 14 elements | Accepted, the stated long-term destination |

Hybrid is the floor, not the target. Today only Town Name and Country are mandatory. Street Name, Building Number and Post Code are recommended. Those recommendations are exactly the kind that become requirements in a later rulebook, and the CPMI and PMPG harmonised data model already points at an end-2027 horizon for the broader address structure.

The design implication is direct. Modeling the full `PostalAddress24` field set now costs almost nothing beyond the hybrid work already required. Discovering in 2027 that Street Name became mandatory while the system stores it as free text costs a data migration across live customer records.

---

## What Actually Breaks in an Existing Integration

The deadline is usually presented as a messaging change. In practice the failure points sit upstream of the message layer, in systems nobody flagged as payment infrastructure.

**Onboarding forms.** A single free-text address box on a signup screen guarantees unstructured data entering the system at origination. Every downstream fix is remediation of a problem the form created. Structured capture at origination is the only version that stops the bleeding.

**Customer master data.** Historical records hold addresses collected under the old form. Swift's own figures put roughly 65% of payment messages still carrying unstructured addresses as of March 2026. A backfill is a data project with a completion date, not a sprint task, and it needs a defined quality bar for what counts as successfully parsed.

**Corporate file ingestion.** Bulk payment files from corporate ERP systems arrive shaped by the client's data model, not yours. Rejecting them at the boundary is correct behavior and a commercial conversation at the same time. The rejection reason has to be specific enough for the client's operations team to act on, which means the API error contract needs an address-level failure code rather than a generic validation error.

**Third-party enrichment.** A geocoding or address-validation vendor can raise the parsed share, and it introduces a new question: what happens when the vendor returns a Town Name that differs from what the customer entered. That is a requirement, not an implementation detail, and it belongs in the spec with an explicit answer.

**Screening and reconciliation.** Sanctions screening tuned against concatenated address strings behaves differently against discrete fields. False positive rates move. Anyone who treats the address change as purely a payments concern will find out during the first screening review after go-live.

---

## Questions a Specification Has to Answer

Write these into the requirement rather than leaving them to be discovered in testing.

1. Where in the flow is address structure enforced, at origination or at message construction?
2. What happens to a payment initiated before the deadline with a value date after it?
3. Which error is returned when a submitted address cannot be structured, and how specific is the message?
4. What is the fallback when a third-party parser returns low confidence, reject or route to manual review?
5. Which internal system is the source of truth for a customer address once three systems hold a copy?
6. How is the change communicated to corporate clients submitting bulk files, and how far ahead?

---

## Field Reference

The minimum compliant set inside `PstlAdr`:

```xml
<PstlAdr>
  <TwnNm>Bogota</TwnNm>
  <Ctry>CO</Ctry>
</PstlAdr>
```

Hybrid adds free text alongside the structured minimum:

```xml
<PstlAdr>
  <TwnNm>Bogota</TwnNm>
  <Ctry>CO</Ctry>
  <AdrLine>Carrera 7 No 71-21</AdrLine>
</PstlAdr>
```

Fully structured replaces `AdrLine` with discrete elements:

```xml
<PstlAdr>
  <StrtNm>Carrera 7</StrtNm>
  <BldgNb>71-21</BldgNb>
  <PstCd>110231</PstCd>
  <TwnNm>Bogota</TwnNm>
  <CtrySubDvsn>Cundinamarca</CtrySubDvsn>
  <Ctry>CO</Ctry>
</PstlAdr>
```

`Ctry` takes a two-letter ISO 3166-1 alpha-2 code. A country name in that field is a validation failure, and it is the single most common mistake in early structured-address testing.

---

## Sources

* Swift, removal of unstructured address guidance and CBPR+ SR 2026 Usage Guidelines
* Swift, ISO 20022 in bytes for payments, on the November 2025 coexistence milestone and the hybrid grace period
* J.P. Morgan ISO 20022 migration guidance on the November 14, 2026 dual requirement
* PMPG and HVPS+ market practice publications on the structured address roadmap

Standards move. Verify against the current Usage Guideline before writing a requirement against anything in this pack.

---

## Related Artifacts

* [knowledge-packs/cross-border-payments-glossary.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/cross-border-payments-glossary.md) - Definitions for agent, party, debtor and the other role terms used above
* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - The intake questions to run before writing any of the requirements this pack implies
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Rejection on address validation is an unhappy path that needs mapping before build

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
