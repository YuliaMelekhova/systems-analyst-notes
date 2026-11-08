<!-- LinkedIn: -->

# Judgment Log Template

**Series:** Systems Analyst Notes  
**Post:** 69  
**Phase:** 9 Reflection  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Records what a human reviewer did with an AI output: what they were shown, what they checked outside the agent, and what they changed. Reach for it when a review step exists on paper and someone needs evidence that judgment was possible, not only that an approval was clicked.

---

## 1. Which reviews get an entry

A log with an entry for every click becomes the thing nobody reads. Write an entry when the output feeds a decision, a document or a record that someone else relies on.

| Checkpoint tier | Entry |
|---|---|
| Auto-proceed | None. Sample a few per month if volume allows |
| Lightweight confirm | A sampled entry, for example one in ten |
| Explicit approval | Every time |
| Blocked | Every time, and the entry names who released it |

The tiers come from the five-tier checkpoint spec. If your checkpoints are named differently, keep the principle: the more consequential the action, the fewer reviews go unrecorded.

---

## 2. The fields

Ten fields. The first four identify the review, the next four show whether judgment was possible, and the last two record what happened.

| Field | What goes in it | What it catches |
|---|---|---|
| `entry` | ID and date | Entries that cannot be found again |
| `output_ref` | Reference to the agent output, with the model version | A decision that cannot be traced to the output behind it |
| `reviewer` | Name and role of the individual, never a team | An approval nobody personally made |
| `shown` | What the reviewer saw: the summary, the full trace, or the source documents | Approvals given on a surface that made doubt impossible |
| `independent_source` | Where the reviewer looked outside the agent: a test, the source document, the owner of the system. `none` is a valid entry | Agreement mistaken for verification |
| `left_out` | What the output omitted that the reviewer knew to look for. `nothing found` is a valid entry | Omissions, which no line-by-line check can see |
| `assumed_constraint` | A rule the output or an automated check relied on that nobody wrote down | A check that passes against the wrong constraints |
| `load` | Items in the queue and minutes available for this one | Review quality that fell with volume |
| `verdict` | accepted, changed, rejected or escalated | The share of outputs that never meet resistance |
| `override_reason` | Why the output was changed, rejected, or escalated. Blank only when accepted | Corrections that never feed back into the next run |

---

## 3. The entry to copy

```
entry:               JL-0000, YYYY-MM-DD
output_ref:          [agent output ID], [model version]
reviewer:            [name], [role]
shown:               [summary | full trace | source documents]
independent_source:  [what was checked outside the agent, or none]
left_out:            [what the output omitted, or nothing found]
assumed_constraint:  [the unwritten rule, or none identified]
load:                [items in queue], [minutes available]
verdict:             [accepted | changed | rejected | escalated]
override_reason:     [why, or blank when accepted]
```

---

## 4. A worked example

Illustrative and genericized, not a record of a real review. An agent extracts requirements from a 90-minute workshop transcript on settlement retries.

```
entry:               JL-0031, 2026-08-18
output_ref:          RQ-extract-0412, model version pinned in the run log
reviewer:            Sam Rivera (fictional), Senior analyst, settlement platform
shown:               summary only
independent_source:  transcript, minute 41, and the retry limit ADR
left_out:            Mexico corridor exception, mentioned once mid-transcript
assumed_constraint:  retry limit of 3 applies to every corridor
load:                14 items in queue, 20 minutes
verdict:             changed
override_reason:     Corridor bank confirmed intermittent timeouts on its side; limit is 5 for Mexico
```

Two details in the entry matter more than the verdict. The reviewer was shown a summary only, which is why the exception was invisible until they opened the transcript. And the constraint "applies to every corridor" was assumed by the output and never stated, so a check limited to that assumption could have missed the exception.

---

## Reading the Log

Review the log monthly. Four steps cover most of what it can tell you.

**Step 1: Count `independent_source` fields marked `none`; flag blanks as incomplete entries.** A high share means independent verification is not documented; investigate why.

**Step 2: Compare the accepted share with the load.** Near-total acceptance under a heavy workload warrants a sample review; the acceptance rate alone does not establish poor review quality.

**Step 3: Group `shown` against `left_out`.** Check whether recorded omissions cluster where the reviewer saw only a summary.

**Step 4: Read the override reasons for patterns.** Repeated reasons warrant investigation of the prompt, retrieval, rule table, source material, and review process before assigning a cause.

---

## What the log does not prove

A full log shows that review was attempted and how. It does not show that the review was right, and it does not replace a reviewer with the expertise and authority to act on what they find.

Three sources shaped the field set. A Microsoft Research and Carnegie Mellon survey of 319 knowledge workers linked higher confidence in AI with less critical thinking, and the answers were self-reported. The Financial Stability Board's October 2026 sound practices are nonbinding and warn that human involvement alone does not guarantee effective oversight. The US Office of the Comptroller of the Currency framework of November 4, 2026 (Bulletin 2026-54) describes what a meaningful review may need, and it is guidance for examiners, not a requirement for banks.

---

## Related Artifacts

* [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) - The five tiers that decide which reviews earn an entry
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - The five-column change log, where a reviewer's correction gets its own row
* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - Where a decision that a reviewer overturned gets recorded as a decision

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
