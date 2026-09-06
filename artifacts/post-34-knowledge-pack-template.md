<!-- LinkedIn: -->

# Knowledge Pack Template

**Series:** Systems Analyst Notes  
**Post:** 34  
**Phase:** 5 Bringing AI Into the Workflow  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Turns a raw source, a transcript, a recorded meeting, or an existing document, into a Knowledge Pack a retrieval pipeline can find and use correctly. Reach for it before writing any new Pack, including one built from a document that already exists.

---

## 1. What earns a source a Pack

Not every transcript or document needs to become a Pack. A source earns one when it answers a question more than one future task is likely to ask, and when the answer is stable enough to stay correct for weeks rather than hours.

A single client call about one edge case is a source. A client call that settles how a whole class of settlement failures gets handled is a Pack. The test is reuse, not length.

---

## 2. Required metadata

Every Pack opens with a metadata block, in addition to the standard header block defined in `anti-ai-artifacts.md`. These fields exist for the retriever, not for a human skimming the page.

| Field | Rule |
|---|---|
| Title | States the single topic the Pack covers. Never a list of topics joined by "and". |
| Tags | 3 to 6 keywords a query would actually use, not a restatement of the title. |
| Domain | One of the five ADF branches, or the business domain the Pack sits in (payments, compliance, onboarding). |
| Date | The date the underlying facts were true, which is not always the date the Pack was written. |
| Version | Increments when the underlying facts change. A Pack describing a rule that later changes gets a new version, not a silent edit. |

A Pack with any of these missing is not ready to publish, regardless of how complete the body reads.

---

## 3. Body: one topic, chunked for meaning

The body covers a single coherent topic. A Pack that starts drifting into a second topic is two Packs that happen to share a title.

Four rules keep a chunk meaningful rather than accidental:

**Section boundaries follow ideas, not length.** A heading marks where one sub-question ends and the next begins. Splitting mid-argument to hit a word count produces a chunk that answers half a question.

**Each section stands alone.** A retriever pulls one section at a time, not the whole Pack. A section that only makes sense after reading the section before it will get retrieved without that context, and the answer it produces will be wrong in a way nobody can trace back to the Pack.

**Headings name the question, not a category.** "Retry Limit After a Correspondent Timeout" retrieves. "Overview" does not, no matter how well the section under it is written.

**Examples stay genericized.** A worked example built from a real client scenario gets stripped of anything that identifies the client, the exact figures, or the specific counterparties, and rebuilt as a plausible but fictional fintech scenario. The pattern is what the Pack is for. The client's name is not.

---

## 4. Source traceability

A Pack built from a transcript or a recorded meeting carries a source block naming where each claim came from:

```
Source: Client architecture review, 2026-08-19
Segment: Settlement retry logic, minutes 14 to 22
Extracted as: Sequence diagram (post-25-sequence-diagram.mmd),
              retry field schema, changelog entry
```

This is what separates a Knowledge Pack from a plausible-sounding summary. A claim earns its place in the Pack only with a traceable source. Without one, it stays a follow-up question for whoever made the claim in the first place.

---

## 5. Test query set

Every Pack ships with a minimum of three representative questions it should answer correctly, written before the Pack is considered done rather than after a retrieval failure surfaces one.

```yaml
test_queries:
  - question: "What is the retry limit on a failed settlement instruction?"
    expected: "States the current limit and cites the ADR that set it."
  - question: "Who approved raising the retry limit, and why?"
    expected: "Names the approving role and the corridor issue that drove it."
  - question: "Does this Pack apply to the Mexico corridor specifically?"
    expected: "States the corridor scope explicitly, not by omission."
```

Writing the test set only proves the questions exist. Running it against the Pack is what proves the Pack actually works.

---

## 6. Worked example: from two transcripts to three artifacts

A genericized version of how this runs in practice, using two source conversations that were never intended as documentation.

A client call surfaces a recurring settlement delay on one corridor. An architecture review, held the same week, settles how the retry logic should change to handle it. Neither transcript was written for anyone outside the room.

From those two transcripts, three artifacts come out the other side, each traceable to a specific segment:

**A sequence diagram**, showing the retry flow between the orchestrator and the correspondent bank, drawn from the architecture review's whiteboard discussion.

**A field schema**, capturing the retry count and backoff fields the architects agreed on, in JSON.

**A changelog entry**, using the Post 24 template, recording what changed in the retry policy and why.

The Knowledge Pack itself is a fourth artifact: the write-up of the decision, with the metadata, the source trace, and the test queries this template requires. It is what a future agent retrieves when someone asks why the retry limit is what it is, six months from now, long after the meeting is forgotten.

---

## 7. Quality gate before publishing

Four checks, all of them cheap, before a Pack is considered ready.

1. Does the metadata block carry all five required fields, with a domain and tags a real query would use?
2. Does every claim in the body trace back to a named source, rather than to general knowledge the writer already had?
3. Does the Pack cover one topic, checked by whether every section still makes sense if retrieved on its own?
4. Does the Pack pass its own test query set, checked by actually running the retrieval rather than by inspection?

A Pack that fails check 3 is the one that reads well end to end and still retrieves badly, because nobody asked whether each piece survives on its own.

---

## Related Artifacts

* [artifacts/post-25-sequence-diagram.mmd](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.mmd) - One of the artifact types a Knowledge Pack workflow produces, when the source describes a system conversation
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - The format used to log a Pack's version change once the underlying facts move

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
