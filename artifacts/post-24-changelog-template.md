<!-- LinkedIn:  https://www.linkedin.com/posts/yuliamelekhova_systemsanalysis-businessanalysis-documentation-share-7494722187745165312-VhCO/-->

# Requirement Change Log Template

**Series:** Systems Analyst Notes  
**Post:** 24  
**Phase:** 4 APIs as Products  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

A five-column log that records why a requirement changed and what else had to move, which page history does not capture. Reach for it on any requirement that will still be referenced after the feature ships.

---

## The table

Paste this at the bottom of the requirement itself. Not in a separate document, not in a folder of change logs. A log that lives apart from the artifact it describes is a second thing to keep in sync, and it loses that race.

| Date | What changed | Why | Requested by | What else had to change |
|---|---|---|---|---|
| YYYY-MM-DD | | | | |

Newest row at the bottom. Append only. A change log with edited history is a document with two versions of the truth in it.

---

## Column definitions

**Date.** ISO format, `YYYY-MM-DD`. The date the change was agreed, not the date someone got around to writing it down. Where those differ by more than a few days, that gap is itself worth noticing.

**What changed.** The old value and the new value, both stated. "Updated the retry limit" is a note to self. "Retry limit raised from 3 to 5" is a record. If the change is structural rather than a value, name the section: "Acceptance criterion 4 removed, covered by AC-2 after rewrite."

**Why.** The reason, not the mechanism. "Because the PO asked" is the mechanism. "Mexico corridor bank confirmed intermittent timeouts on their side" is the reason. This column is the entire point of the log, and it is the one that gets filled in laziest.

**Requested by.** A named person and their role. Roles change, people move, and a row that says "Compliance" tells you nothing in eighteen months.

**What else had to change.** Every downstream artifact that moved as a result: contracts, ADRs, test cases, integration specs, configuration. This column is what turns the log into a traceability record instead of a diary. An empty cell here is a claim that nothing downstream was affected, and that claim is usually wrong.

---

## When a row is required

1. Any change to an acceptance criterion, in wording or in value.
2. Any change to a threshold, limit, timeout, retry count or currency amount.
3. Any change to scope, including removal.
4. Any change made after the requirement reached baseline, without exception.
5. Any decision to leave something unchanged after it was formally challenged. The row records that the question was asked and answered.

Typo fixes, formatting and reordering do not earn a row. If the meaning did not move, the log does not need to know.

---

## Worked example

A settlement retry limit, four months of real edits.

| Date | What changed | Why | Requested by | What else had to change |
|---|---|---|---|---|
| 2026-05-04 | Retry limit set at 3 for all corridors | Default carried over from the card processing flow, no corridor-specific analysis done | Backend lead, at drafting | None, initial baseline |
| 2026-06-11 | Backoff changed from fixed 30s to exponential, base 2s | Fixed interval was retrying inside the bank's own outage window and burning all three attempts in 90 seconds | Backend lead, after the June incident | Settlement service config, integration spec section 4.2 |
| 2026-08-18 | Retry limit raised from 3 to 5, Mexico corridor only | Mexico corridor bank confirmed intermittent timeouts on their side, not ours. Three attempts were exhausting before their recovery window closed | Compliance lead, after the August incident review | Settlement service config, ADR-014, integration spec section 4.2, two test cases, `camt.053` daily report column set |
| 2026-08-29 | Limit left at 3 for Brazil and Colombia after review | Same question asked for the other two corridors. Neither shows the timeout pattern, and a higher limit widens the duplicate-settlement window | Compliance lead | None. Row exists so the question is not reopened from scratch |

Four rows, and the fourth one is the reason the log is worth keeping. Without it, the same discussion happens again in November and nobody remembers it was already settled.

---

## Why not page history

Most wikis version pages already, so the objection is reasonable. Page history gives you what changed and when. It gives you neither why nor what else moved, and those are the two questions anyone actually arrives with.

There is a second reason, newer than the first. Anything retrieving a requirement automatically, whether that is a search index or an agent drafting from it, cannot tell a rule that has held for two years from one rewritten three times this quarter. Both read as equally settled prose. A change log puts volatility in the artifact itself, where retrieval can see it.

---

## The discipline this replaces

Git enforces this behavior by making it impossible to change a file without leaving a record. A table enforces it only if the team agrees the row is not optional. That agreement is the whole implementation. Everything else here is five columns.

---

## Related Artifacts

* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - A change that reopens an architectural decision gets a row here and a record there
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - The last column is easier to fill when the decomposition already names the affected services
* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - Contract changes are the ones most often assumed to be non-breaking
* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - A requirement that fails intake tends to generate change rows within a sprint

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
