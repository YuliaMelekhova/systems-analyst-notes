<!-- LinkedIn: -->

# Mandated Change Register

**Series:** Systems Analyst Notes  
**Post:** 29  
**Phase:** 4 APIs as Products  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Tracks upcoming regulatory obligations that change an API contract on somebody else's schedule. Companion to the Post 28 versioning policy, which covers the changes the team controls: this register covers the changes it does not.

---

## How to use this file

One row per regulatory obligation in `post-29-mandated-change-register.csv`, not per regulation. PSD3 alone produces four rows here, because each obligation lands in the contract differently and gets classified as breaking or non-breaking on its own.

**Date Status is the column that matters most.** An effective date on a mandate the team does not control is a claim, not a fact, until the regulator or network confirms it. Two values cover almost every case:

* **Estimated.** Built from a publication date plus a known transition length, before the publication itself is final. Revisit the estimate once the anchor date is confirmed.
* **Deferred.** A date existed, and the body that set it moved it. Record the deferral date, who moved it, and when the next update is promised. Never delete the row.

A row never gets removed because a date moved. It gets its Date Status updated and its remediation work kept live. The ISO 20022 rows in this register are the worked example: Swift set November 14, 2026, then deferred it on August 27, 2026, with an update promised no later than December. The fields, the owners and the breaking classification did not change. Only the date did.

**Review cadence.** Check this register whenever a tracked body publishes an update, and at minimum monthly for any row marked Estimated or Deferred. A row that has sat unreviewed for a full quarter is a register nobody is actually using.

---

## Column definitions

| Column | What goes here |
|---|---|
| Regulation | The specific obligation, not just the umbrella regulation. "PSD3" is not a row. "PSD3: IBAN and Name Verification" is. |
| Effective Date | The date as currently known, stated with the same precision the source uses. Do not round an estimate into a false certainty. |
| Date Status | Confirmed, Estimated or Deferred, plus the one sentence that justifies the label. |
| Endpoints Affected | The actual path, not the service name. |
| Fields Added or Changed | Specific enough that an engineer could diff the schema against it. |
| Breaking or Non-Breaking | Classified against the Post 28 policy, section 3. |
| Client Notice Required | Yes or no, plus the condition that triggers it if it is not automatic. |
| Accountable Owner | One named role or person. A regulation with two owners has not been assigned yet. |

---

## Related Artifacts

* [artifacts/post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) - The breaking versus non-breaking classification every row here is checked against
* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - PostalAddress24 and PayeeVerificationResult, the two schemas the first and fifth rows change
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Section 6 asks whether any cell still reads UNKNOWN without a name attached, the same discipline this register applies to Accountable Owner

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
