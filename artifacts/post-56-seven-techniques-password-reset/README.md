<!-- LinkedIn: -->

# Seven Ways to Document One Requirement

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Documents one genericized requirement, a password reset by one-time code, in seven forms so the same facts can be compared across techniques. Reach for it when choosing which technique a given reader needs, and for checking that one value does not drift between documents.

---

## The requirement

REQ-AUTH-014. A customer who has forgotten a password resets it with a one-time code sent by SMS to the mobile number on the account.

## Which lens for which reader

| Reader | Open | Question it answers |
|---|---|---|
| Product team | `user-story.md`, `wireframe.md` | Why does this exist, and what does the customer see? |
| Testers | `use-case.md` | In how many ways can this go wrong? |
| Ops | `bpmn.md` | Which system acts at each step, and who waits? |
| Developers | `decision-table.csv`, `data-mapping.md` | What happens for each input, and what gets stored? |
| Security and compliance | `business-rules.md` | Which constraints apply, and who owns each one? |

## What each lens makes hard to miss

| Lens | Hard to miss with it |
|---|---|
| Use case | The SMS gateway can fail, and the customer must not be able to tell |
| Wireframe | The screen has to say something when the number belongs to no account |
| Decision table | Every combination of conditions has an outcome, or a visible gap |
| Data mapping | The failed-entry counter needs a column, a starting value and a reset rule |

## One home for every value

The 5-minute window appears in all seven documents here. `business-rules.md` owns it, under the ID BR-03, and every other file that repeats the number carries the ID next to it. The same holds for 3 entries, 30 minutes, 60 seconds, 3 requests per hour and 12 characters. When a value changes, the rule is edited first, and the `Appears in` column lists the files to update.

## How to adapt it

Step 1: Write the rules list first and give every value an ID.

Step 2: Draft the use case, and move to the BPMN flow once the exception list stops growing.

Step 3: Build the decision table from the rules, one row per combination of conditions.

Step 4: Derive the data mapping last, since it exposes the fields nobody mentioned.

The user story and the wireframe slot in wherever the product team needs them. Drop any lens whose reader does not exist for your requirement.

---

## Related Artifacts

* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Where the exception flows in the use case come from
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - Records which of these files moved when a rule value changes
* [artifacts/post-25-sequence-diagram.mmd](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.mmd) - A sequence view of a similar flow, for when message order matters more than lanes
* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - Where mapped fields become a typed contract

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
