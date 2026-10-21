<!-- LinkedIn: -->

# Cross-Functional Glossary

**Series:** Systems Analyst Notes  
**Post:** 60  
**Phase:** 8 Scaling  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

Records every meaning a shared word carries across functions, with one owner and one name per meaning, so a requirement never leans on a bare term that two teams read differently. Reach for it when a word in a requirement, a status field or a report is used by more than one team.

---

## What the CSV holds

[artifacts/post-60-cross-functional-glossary.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-60-cross-functional-glossary.csv) has one row per meaning, not one row per term. A word with three live meanings has three rows. The worked example covers four terms from a cross-border payments platform: settled, customer, approved and active, three meanings each.

| Column | What goes in it |
|---|---|
| `term` | The bare word as people say it. The same value repeats across the rows for that word. |
| `qualified_name` | The name that replaces the bare word in requirements. Lowercase with underscores, unique across the file. |
| `function` | The team that uses this meaning. |
| `definition` | One or two sentences, in words someone outside the team can follow. |
| `evidence` | The event, status or record that shows the meaning is true. A meaning with no observable evidence is an opinion. |
| `owner` | One role. Never a channel, a distribution list or the word "everyone". |
| `conflicts_with` | The `qualified_name` of every other row under the same term, separated by semicolons. |
| `status` | `qualified` when the bare word is banned and the qualified name is required. `canonical` when only one meaning is live and the bare word is allowed. `retired` when no team uses the meaning anymore. |
| `last_reviewed` | An ISO date. Moves forward whenever the definition or the evidence changes. |

The file is plain text on purpose. A person can read it in a diff, and a retrieval step can filter on `qualified_name` or `status` before an agent sees any document that uses the word.

---

## Review gate

Five checks before a row is added or changed. All of them are cheap, and the third one catches the most.

1. Every row under a term with more than one meaning has status `qualified`. The bare word appears in no other requirement once the row is merged.
2. Every row names exactly one owner, and that owner is a role a person can be asked.
3. `conflicts_with` is symmetric. If row A names row B, row B names row A, and neither list is missing a sibling.
4. `evidence` points at something a system produces or a person can check, not a restatement of the definition.
5. A changed definition updates `last_reviewed` in the same commit and adds a row to the change log from Post 24.

A row records a meaning that a team actually uses. A team that misuses a word is a training issue and does not earn a row.

---

## Adapting it

Step 1: Collect the candidates. Search the last quarter of incident reviews, support tickets and requirement comments for the phrase "what do you mean by". The words that show up more than once are the first rows.

Step 2: Ask each function for its definition separately. Do this before putting the teams in one room, because a group conversation produces a compromise that nobody actually uses.

Step 3: Name each meaning. Pick names that say what happens, such as `partner_confirmed`, and not names that say who cares, such as `engineering_settled`.

Step 4: Replace the bare word. Update the requirement, the status field and the report label, then record the change. A glossary row that no document links to has not changed anything.

When a meaning has real reach, record the decision to retire or rename the bare word as an ADR, using the template from Post 23.

---

## Related Artifacts

* [artifacts/post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) - Section 3 names the meaning change as the breaking change schema tools miss, and this file is where each meaning is written down
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - The five columns that record a changed definition and what else had to move
* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - Where the decision to rename or retire a widely used word is recorded
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Names the owner of every service, which is where most glossary owners come from

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
