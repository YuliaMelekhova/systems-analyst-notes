<!-- LinkedIn: -->

# Prompt: BRD Gap Analysis

**Series:** Systems Analyst Notes  
**Post:** 76  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Reviews a draft BRD for ambiguous terms, missing owners, unstated dependencies and absent failure scenarios, and turns the findings into questions for the next workshop. Reach for it before a draft goes to review, so the obvious gaps are found by you and not by the developers.

---

## When to use it

Use it on any draft requirements document, including one you wrote yourself. The prompt states the review criteria and does not reveal whether you think the draft is ready, so the review is an assessment and not an endorsement.

Before you paste anything, remove customer names, account numbers and other personal data. Replace each value in square brackets with your own.

## The prompt

The limits sit first, each source sits in its own labeled block, and the request comes last. Models tend to use the start and the end of a long input better than the middle, so a rule buried mid-document is the one most likely to slip.

```text
TASK AND LIMITS
Review the draft BRD below. Do not rewrite it. Assess it against these four criteria:
1. Ambiguous terms: words a reader could interpret in more than one way.
2. Missing owners: requirements or failure paths with no named role responsible.
3. Unstated dependencies: other systems, teams, rules or data a requirement relies on without saying so.
4. Failure scenarios: what happens when the requirement cannot be met.
Hard limits:
- Assume nothing about whether the draft is ready.
- Quote the phrase you are questioning, then say what is missing.
- Rank each finding High, Medium or Low by how much it could block the build, with a one-line reason.
- If a criterion yields no finding, say so. Do not invent one.

CONTEXT
Product: [product name]
Reviewers who will read the findings: [for example, product owner, engineering lead]

SOURCES
<brd>
[paste the draft BRD here]
</brd>

REQUEST
List findings under each criterion, weakest section first. End with Questions for the Next Workshop, each addressed to a role.
```

## Worked example: before and after

**Before: the thin prompt.**

```text
Review this BRD and tell me if it is ready.

[BRD pasted below]
```

What tends to come back is a confident, generic result with no sources and gaps filled by plausible text. It reads like a decision, and nobody can tell which parts the input supported.

**After: the same input, the saved prompt.** The limits and the request stay as saved above. Only the context and the sources change.

```text
CONTEXT
Product: cross-border payments platform
Reviewers who will read the findings: product owner, engineering lead

SOURCES
<brd>
BR-04 The system shall send a notification when a payment is settled.
BR-05 Failed payments are retried a reasonable number of times.
BR-06 Customers in supported countries can pay in local currency.
BR-07 Compliance checks happen before settlement.
</brd>
```

**What a reviewable output looks like.** This excerpt was written by hand to show the shape. It is not the output of a model run.

```text
Ambiguous terms
High   BR-04 "settled": more than one meaning is possible (delivered, confirmed by the partner bank, posted to the ledger). No definition given.
High   BR-05 "a reasonable number of times": cannot be tested.
Medium BR-06 "supported countries": no list given.

Missing owners
Medium BR-05: no role is responsible for a payment that still fails after the last retry.

Unstated dependencies
High   BR-07 "Compliance checks": which checks, at which stage, and what happens when one fails are not stated.

Failure scenarios
No finding beyond those listed above.

Questions for the Next Workshop
1. Which event does "settled" mean here? Role: Finance.
2. How many retries, at what interval? Role: Engineering.
3. Which countries are supported at launch? Role: Product.
4. Which compliance checks run before settlement, and what stops the payment? Role: Compliance.
```

## Check the output

* Each finding quotes the phrase it questions, so you can find it in the draft.
* Open two findings against the draft to confirm they are real, not invented.
* The High findings are the ones that would stop a developer from building.
* Every workshop question names a role that can answer it.

## Keeping it current

Store the prompt in a file, not in a chat history. Add an owner and a last-reviewed date in your own copy, and change the limits when a reviewer finds a failure the prompt did not prevent.

---

## Related Artifacts

* [artifacts/post-76-five-analyst-prompts/workshop-notes-to-brd.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-76-five-analyst-prompts/workshop-notes-to-brd.md) - Produces the draft that this prompt then checks
* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - Readiness checks to run before a requirement is written, not after
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - A fuller method for the failure scenarios this review looks for
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Helps name the owner and the dependencies the review finds missing

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
