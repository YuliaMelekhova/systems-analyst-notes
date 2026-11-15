<!-- LinkedIn: -->

# Prompt: Features to User Stories

**Series:** Systems Analyst Notes  
**Post:** 76  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Converts feature descriptions into user stories with Given/When/Then acceptance criteria, one story per behavior, and lists what the features left open. Reach for it when a feature arrives as a paragraph and the team needs something it can estimate and test.

---

## When to use it

Use it when features are described in prose and no one has yet split them into behaviors. Paste your glossary terms in the context block so each word keeps one meaning across every story.

Before you paste anything, remove customer names, account numbers and other personal data. Replace each value in square brackets with your own.

## The prompt

The limits sit first, each source sits in its own labeled block, and the request comes last. Models tend to use the start and the end of a long input better than the middle, so a rule buried mid-document is the one most likely to slip.

```text
TASK AND LIMITS
Convert each feature description below into user stories with acceptance criteria.
Format: "As a [role], I want [action] so that [outcome]", then criteria in Given / When / Then form.
Hard limits:
1. Write one story per distinct behavior. Split a feature that contains two.
2. Use a role named in the feature text or in the roles list. If none fits, write "Role not stated" and ask.
3. Give every story at least one criterion for the normal case and one for a failure case.
4. Do not invent numbers, limits, status names or error messages. Write "Not stated" and ask.

CONTEXT
Product: [product name]
Roles: [for example, customer, support agent, compliance officer]
Terms with one meaning each: [for example, settled = funds posted to the ledger]

SOURCES
<features>
[paste the feature descriptions here]
</features>

REQUEST
Write the stories for every feature. Then list each question the features left open, addressed to a role.
```

## Worked example: before and after

**Before: the thin prompt.**

```text
Write user stories for this feature.

[feature pasted below]
```

What tends to come back is a confident, generic result with no sources and gaps filled by plausible text. It reads like a decision, and nobody can tell which parts the input supported.

**After: the same input, the saved prompt.** The limits and the request stay as saved above. Only the context and the sources change.

```text
CONTEXT
Product: cross-border payments web app
Roles: customer, support agent
Terms with one meaning each: settled = funds posted to the ledger

SOURCES
<features>
F1: After a customer submits a payment, the app shows its current status on the payment page.
</features>
```

**What a reviewable output looks like.** This excerpt was written by hand to show the shape. It is not the output of a model run.

```text
ST-01  As a customer, I want to see the status of a payment I submitted so that I know whether to wait or contact support.
  Given a submitted payment, when I open the payment page, then I see its current status.
  Given the status service does not answer, when I open the payment page, then I see "Status unavailable" and the time of the last known status.

Questions
1. Which status names does the customer see? Role: Product.
2. Is "settled" shown to the customer, and under which definition? Role: Finance.
3. How old can the last known status be before the page stops showing it? Not stated. Role: Engineering.
```

## Check the output

* Each story covers one behavior, and a feature with two behaviors became two stories.
* Every story has a failure criterion, not only the normal case.
* No number, status name or message appears that the features do not state.
* Each question names a role that can answer it.

## Keeping it current

Store the prompt in a file, not in a chat history. Add an owner and a last-reviewed date in your own copy, and change the limits when a reviewer finds a failure the prompt did not prevent.

---

## Related Artifacts

* [artifacts/post-76-five-analyst-prompts/acceptance-criteria-to-uat-cases.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-76-five-analyst-prompts/acceptance-criteria-to-uat-cases.md) - Takes the criteria from these stories and builds the test cases
* [artifacts/post-76-five-analyst-prompts/workshop-notes-to-brd.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-76-five-analyst-prompts/workshop-notes-to-brd.md) - Produces the business requirements these features come from
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - A fuller method for the failure criteria every story needs
* [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) - Checks that a feature is ready before stories are written for it

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
