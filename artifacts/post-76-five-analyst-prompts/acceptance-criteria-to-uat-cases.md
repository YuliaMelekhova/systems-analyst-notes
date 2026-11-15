<!-- LinkedIn: -->

# Prompt: Acceptance Criteria to UAT Cases

**Series:** Systems Analyst Notes  
**Post:** 76  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Generates user acceptance test (UAT) cases from acceptance criteria, with boundary cases on every number and a list of criteria that never said what should happen. Reach for it before UAT planning, while the criteria can still be fixed cheaply.

---

## When to use it

Use it when criteria exist but the test cases do not. It also works as a quality check on the criteria themselves, because every "Expected result not stated" line is a defect in the criteria, not in the test.

Before you paste anything, remove customer names, account numbers and other personal data. Replace each value in square brackets with your own.

## The prompt

The limits sit first, each source sits in its own labeled block, and the request comes last. Models tend to use the start and the end of a long input better than the middle, so a rule buried mid-document is the one most likely to slip.

```text
TASK AND LIMITS
For each acceptance criterion below, write UAT test cases covering the positive path, the negative path and the edges.
Hard limits:
1. Every number or limit in a criterion gets three boundary cases: just under, exactly at, just over.
2. Each case has an ID, the criterion ID, preconditions, steps, expected result and a type (positive, negative or edge).
3. Take expected results only from the criteria. If a criterion does not say, write "Expected result not stated" and add a question.
4. Write no cases for behavior that no criterion mentions. List such ideas under Possible Missing Criteria.

CONTEXT
Feature: [feature name]
Test environment: [for example, staging with a test SMS gateway]

SOURCES
<criteria>
[paste the acceptance criteria with their IDs here]
</criteria>

REQUEST
Write the test cases, then the questions about unstated results, then Possible Missing Criteria.
```

## Worked example: before and after

**Before: the thin prompt.**

```text
Write test cases for these acceptance criteria.

[criteria pasted below]
```

What tends to come back is a confident, generic result with no sources and gaps filled by plausible text. It reads like a decision, and nobody can tell which parts the input supported.

**After: the same input, the saved prompt.** The limits and the request stay as saved above. Only the context and the sources change.

```text
CONTEXT
Feature: password reset with a one-time code
Test environment: staging with a test text message gateway

SOURCES
<criteria>
AC-01 A code is valid for 5 minutes after it is sent.
AC-02 After 3 failed code entries the account locks for 30 minutes.
AC-03 A new code can be requested no sooner than 60 seconds after the last one.
</criteria>
```

**What a reviewable output looks like.** This excerpt was written by hand to show the shape. It is not the output of a model run.

```text
UAT-01  AC-01  positive  Enter the code 4 minutes 59 seconds after sending. Expected: code accepted.
UAT-02  AC-01  edge      Enter the code at exactly 5 minutes 0 seconds. Expected result not stated.
UAT-03  AC-01  negative  Enter the code 5 minutes 1 second after sending. Expected: code rejected. The message shown is not stated.
UAT-04  AC-02  edge      Make 2 failed entries, then a correct one. Expected: code accepted. What happens to the counter is not stated.
UAT-05  AC-02  edge      Make 3 failed entries, then try a correct code. Expected: account locked.
UAT-06  AC-02  negative  Enter a fourth code while the account is locked. Expected: account stays locked. Remaining lock time not stated.
(AC-03 cases left out of this excerpt.)

Questions
1. Is a code entered at exactly 5:00 valid? Role: Product.
2. What does the customer see when a code has expired? Role: Product.

Possible Missing Criteria
Whether the failed-attempt counter resets after a successful entry.
```

## Check the output

* Every number in the criteria has its under, at and over cases.
* Each test case traces to a criterion ID that exists.
* Every "Expected result not stated" line has a matching question.
* No case describes behavior that the criteria do not mention.

## Keeping it current

Store the prompt in a file, not in a chat history. Add an owner and a last-reviewed date in your own copy, and change the limits when a reviewer finds a failure the prompt did not prevent.

---

## Related Artifacts

* [artifacts/post-76-five-analyst-prompts/features-to-user-stories.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-76-five-analyst-prompts/features-to-user-stories.md) - Produces the stories and Given/When/Then criteria this prompt turns into tests
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Where the negative and edge scenarios come from before they become cases

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
