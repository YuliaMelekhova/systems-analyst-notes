<!-- LinkedIn: -->

# Prompt: Workshop Notes to BRD

**Series:** Systems Analyst Notes  
**Post:** 76  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Turns raw workshop notes into a draft business requirements document (BRD) where every requirement traces to a note line and every gap is listed as a question. Reach for it right after a workshop, while the notes are still fresh enough to correct.

---

## When to use it

Use it when you hold messy notes or a transcript and need a first draft a reviewer can check against the source. It suits one workshop at a time. For a long transcript, paste only the sections that bear on scope, assumptions and constraints.

Before you paste anything, remove customer names, account numbers and other personal data. Replace each value in square brackets with your own.

## The prompt

The limits sit first, each source sits in its own labeled block, and the request comes last. Models tend to use the start and the end of a long input better than the middle, so a rule buried mid-document is the one most likely to slip.

```text
TASK AND LIMITS
Turn the workshop notes below into a draft business requirements document (BRD).
Hard limits:
1. Use only what the notes state. Do not add facts, numbers, systems or regulations.
2. Where a section needs a fact the notes do not give, write "Not stated" and add a question to Open Questions.
3. Give every requirement an ID (BR-01, BR-02, ...) and the note line it came from.
4. Anything a participant said is out of scope goes under Out of Scope, with who said it.
Sections, in this order: Business Goal, Scope, Out of Scope, Stakeholders, Business Requirements, Assumptions, Constraints, Open Questions.
Mark every assumption as "Assumption" and keep it out of Business Requirements.

CONTEXT
Project: [project name]
Domain: [for example, cross-border payments in these markets: ...]
Readers of the BRD: [for example, product owner, engineering lead, compliance]

SOURCES
<notes>
[paste the numbered workshop notes or transcript here]
</notes>

REQUEST
Write the draft BRD now, following the limits above. Put Open Questions last, ordered by how much each one blocks the build.
```

## Worked example: before and after

**Before: the thin prompt.**

```text
Write a BRD from these workshop notes.

[notes pasted below]
```

What tends to come back is a confident, generic result with no sources and gaps filled by plausible text. It reads like a decision, and nobody can tell which parts the input supported.

**After: the same input, the saved prompt.** The limits and the request stay as saved above. Only the context and the sources change.

```text
CONTEXT
Project: Payout retries
Domain: cross-border payments, partner bank integration
Readers of the BRD: product owner, engineering lead, compliance

SOURCES
<notes>
[1] Product: customers see "failed" when the partner bank times out. We want one automatic retry.
[2] Engineering: a retry needs an idempotency key, or we risk paying out twice.
[3] Compliance: does sanctions screening run again on every retry? Not sure, check.
[4] Product: out of scope for now are manual refunds and the Colombia corridor.
[5] Engineering: partner bank timeout is 8 seconds, they say. Not confirmed in writing.
[6] Decide the retry count next week.
</notes>
```

**What a reviewable output looks like.** This excerpt was written by hand to show the shape. It is not the output of a model run.

```text
Business Requirements
BR-01  The platform retries a failed payout automatically once. Source: [1]
BR-02  A retry reuses the original idempotency key so the payout cannot be paid twice. Source: [2]

Out of Scope
Manual refunds. Colombia corridor. Said by: Product, [4]

Assumptions
Assumption: the partner bank timeout is 8 seconds. Engineering states it, unconfirmed in writing. Source: [5]

Open Questions
1. Does sanctions screening run again on every retry? Owner needed: Compliance. Source: [3]
2. How many retries, at what interval? The notes defer this to next week. Source: [6]
```

## Check the output

* Every requirement has an ID and a note line you can find in the source.
* Nothing appears that the notes do not say. Spot-check three names or numbers against the notes.
* Each "Not stated" has a matching question in Open Questions.
* Each out-of-scope item matches who said it in the notes.

## Keeping it current

Store the prompt in a file, not in a chat history. Add an owner and a last-reviewed date in your own copy, and change the limits when a reviewer finds a failure the prompt did not prevent.

---

## Related Artifacts

* [artifacts/post-76-five-analyst-prompts/brd-gap-analysis.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-76-five-analyst-prompts/brd-gap-analysis.md) - The next step: check the draft for ambiguity before the follow-up workshop
* [artifacts/post-76-five-analyst-prompts/features-to-user-stories.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-76-five-analyst-prompts/features-to-user-stories.md) - Turns the approved business requirements into stories for the team
* [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) - The questions to ask in the workshop before any notes exist
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Failure scenarios to raise in the room so the notes capture them

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
