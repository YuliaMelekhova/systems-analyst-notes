# Document Readiness Rules

**Series:** Systems Analyst Notes  
**Branch:** Templates and Quality Rules  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

The gates a document has to clear before it goes to review, and what a reviewer is entitled to send back unread. Reach for it when a review cycle keeps producing the same corrections, or when nobody can say whether a draft is finished.

---

## Why This Exists

Review time is the scarcest input in a documentation process. A reviewer who spends forty minutes finding that acceptance criteria are missing has spent forty minutes doing something the author could have checked in two.

Readiness rules move that check to the author. They are not a quality bar for the content. They are a completeness bar for the artifact, and the difference matters: a requirement can pass every rule below and still be the wrong requirement. What it cannot do is pass them and waste a reviewer's afternoon on a missing field.

---

## The Gates

### Gate 1: Identity

The document says what it is and where it belongs.

* Title states the subject, not the activity. `Payment Initiation API Contract`, not `API work`.
* Status is one of the defined values, and the value is current.
* Owner is a named person. A team name is not an owner.
* Version follows the versioning rule below.
* Every parent and child link resolves. A link to a page that was renamed is a broken link, and it is the most common failure at this gate.

### Gate 2: Scope

A reader can tell what the document covers without inferring it.

* In-scope statement present.
* Out-of-scope statement present, and it names at least one thing a reasonable reader would have assumed was included. An out-of-scope section that lists only obvious exclusions is decoration.
* Assumptions listed and each one attributed to whoever confirmed it. An unattributed assumption is a guess with formatting.
* Dependencies named with their current state, not just their existence.

### Gate 3: Substance

The content is specific enough to build against and to argue with.

* No unresolved placeholder text anywhere in the body.
* Acceptance criteria defined for every requirement, in a form that can fail.
* Non-functional requirements stated with numbers and a measurement condition. `Fast` fails. `Sub-300ms` fails without the load profile it holds under.
* Error and failure behavior described, not only success behavior.
* Terms used consistently with the glossary, or defined locally with a note explaining why the local definition differs.

### Gate 4: Traceability

Someone six months from now can reconstruct why this exists.

* Linked to the originating request or decision.
* Regulatory or standards references cited to the specific clause, release or usage guideline, not to the standard as a whole.
* Decisions that shaped the document recorded as ADRs, or the document states that no architecturally significant decision was made.
* Threat model linked where the document touches a trust boundary.

### Gate 5: Form

The mechanical checks, last because they are the cheapest to fix and the easiest to spot.

* Diagrams are source, not exported images.
* Tables have headers and no empty required cells.
* Headings follow the template structure for the artifact type.
* Spelling and terminology match American English throughout.

---

## What a Reviewer May Return Unread

Three conditions, and each returns the document with the gate named and nothing else written:

1. Any Gate 1 field missing or stale.
2. Placeholder text present in the body.
3. A requirement with no acceptance criteria.

The point of a short list is that returning a document is cheap and unambiguous. A reviewer arguing about whether something was ready has already spent the time the rule was meant to save.

---

## Status Values

| Status | Meaning | Who can set it |
|---|---|---|
| Draft | Being written. No review expected, no dependency should be built on it. | Author |
| Ready for review | All five gates passed. Reviewer time is now reasonable to request. | Author |
| In review | A reviewer holds it. Author edits pause to avoid reviewing a moving document. | Reviewer |
| Approved | Review complete, comments resolved. Safe to build against. | Reviewer |
| Superseded | Replaced. The link to the replacement is in the header. | Owner |
| Archived | No longer relevant and not replaced. The reason is recorded. | Owner |

`Approved` never reverts to `Draft`. A change to an approved document produces a new version at `Draft`, and the approved version stays readable. That rule is what keeps an implementation team from discovering the spec changed under them mid-sprint.

---

## Versioning

`MAJOR.MINOR`, applied to the document rather than the product.

* MINOR rises on clarification, added examples, corrected typos, and anything that does not change what gets built.
* MAJOR rises on a change to scope, a requirement, an interface, or acceptance criteria. Anything that would make an engineer rebuild something.
* The change log records what changed and why, at every increment. A version number with no change log entry is a version number nobody trusts.

The MAJOR and MINOR distinction only earns its keep if the reader can act on it. Anyone seeing a MINOR bump should be able to skip re-reading. If that is not true, the increment was wrong.

---

## Naming

`[type]-[subject]-[qualifier]`, lowercase, hyphen separated.

* `brd-payment-initiation-latam`
* `adr-023-idempotency-key-strategy`
* `spec-address-validation-service`

No dates in names. No `final`, no `v2`, no `updated`. Those belong to the version field, and putting them in the name is how three documents end up claiming to be the current one.

---

## Applying These to an Inherited Document Set

Running all five gates across an existing set produces a long list and no momentum. A narrower first pass works better.

**Step 1: Run Gate 1 only, across everything.** Identity failures are fast to spot and fast to fix, and they surface which documents have no owner. Ownerless documents are the actual problem underneath most documentation debt.

**Step 2: Run Gate 4 on anything an audit touches.** Traceability gaps cost the most when discovered under time pressure.

**Step 3: Apply all five gates to new documents only, from a stated date.** Retrofitting a large set completely is a project nobody funds. Stopping the growth is achievable this week.

**Step 4: Revisit the old set when something is edited anyway.** A document being changed for a real reason is the cheapest moment to bring it up to standard.

---

## Related Artifacts

* [templates-quality-rules/requirement-antipatterns.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/requirement-antipatterns.md) - The failures that pass every gate here and still break in production
* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - The check that runs before writing, where these run before reviewing
* [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) - Entry and exit criteria per discovery step, which feed Gate 2 and Gate 3

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
