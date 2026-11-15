<!-- LinkedIn: -->

# Prompt: Sprint Status to Executive Update

**Series:** Systems Analyst Notes  
**Post:** 76  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Condenses a sprint's ticket list into a three-bullet executive update with owners and decision dates. Reach for it when a status page of forty tickets has to become something a busy reader finishes in a minute.

---

## When to use it

Use it at the end of a sprint or before a steering meeting, when the audience wants outcomes and decisions rather than ticket IDs. It works best when each ticket line carries a state, an owner and a date.

Before you paste anything, remove customer names, account numbers and other personal data. Replace each value in square brackets with your own.

## The prompt

The limits sit first, each source sits in its own labeled block, and the request comes last. Models tend to use the start and the end of a long input better than the middle, so a rule buried mid-document is the one most likely to slip.

```text
TASK AND LIMITS
Summarize the sprint status below as an executive update with exactly three bullets: Done, Blocked, At risk. End with one line: "Decision needed from you:".
Hard limits:
1. One bullet per heading, 35 words at most each.
2. Every blocked or at-risk item names an owner and the date a decision is needed.
3. Use plain business words. Put ticket IDs in brackets at the end of the bullet.
4. Never soften a blocked item into at risk. If a ticket's status is unclear, write "status unclear" and add it to the last line as a question.

CONTEXT
Audience: [for example, head of product and the finance lead]
Sprint dates: [start and end]

SOURCES
<status>
[paste the ticket list with state, owner and date for each]
</status>

REQUEST
Write the update now. In the last line, give the one decision you need from the reader, or write "None".
```

## Worked example: before and after

**Before: the thin prompt.**

```text
Summarize this sprint status for executives.

[ticket list pasted below]
```

What tends to come back is a confident, generic result with no sources and gaps filled by plausible text. It reads like a decision, and nobody can tell which parts the input supported.

**After: the same input, the saved prompt.** The limits and the request stay as saved above. Only the context and the sources change.

```text
CONTEXT
Audience: head of product, finance lead
Sprint dates: two weeks ending Friday

SOURCES
<status>
PAY-101 Retry limit change - Done
PAY-102 Status page update - Done
PAY-103 Partner bank sandbox access - Blocked, owner Engineering, waiting on bank since day 3
PAY-104 Sanctions rescreen on retry - In progress, owner Compliance, rule not confirmed
PAY-105 Daily settlement report - Done
PAY-106 Colombia corridor test - Not started, depends on PAY-103
</status>
```

**What a reviewable output looks like.** This excerpt was written by hand to show the shape. It is not the output of a model run.

```text
Done: Retry limit, status page and daily settlement report are live. [PAY-101, PAY-102, PAY-105]
Blocked: Partner bank sandbox access, owner Engineering, has waited on the bank since day 3. Decision needed by Monday. [PAY-103]
At risk: Rescreening on retry, owner Compliance, depends on a rule nobody has confirmed, and the Colombia test cannot start until the sandbox opens. Decision needed Wednesday. [PAY-104, PAY-106]
Decision needed from you: Who contacts the partner bank at executive level this week?
```

## Check the output

* The count of tickets behind each bullet matches the ticket list, with none missing.
* Every blocked ticket appears under Blocked, not under At risk.
* Each blocked or at-risk bullet names an owner and a date.
* The last line asks for a decision a reader can actually make.

## Keeping it current

Store the prompt in a file, not in a chat history. Add an owner and a last-reviewed date in your own copy, and change the limits when a reviewer finds a failure the prompt did not prevent.

---

## Related Artifacts

* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Names the owner of each service, which is who to put beside a blocked item
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - Holds the reasons behind scope changes that the sprint update only summarizes

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
