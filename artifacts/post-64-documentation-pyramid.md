<!-- LinkedIn: -->

# Documentation Pyramid

**Series:** Systems Analyst Notes  
**Post:** 64  
**Phase:** 8 Scaling  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Orders documentation into four layers, each resting on the one below, so a team knows what to write next and what each item must cite. Reach for it when there is time for one more document and the choice is open.

---

## 1. The four layers

Read from the bottom. Each layer can only cite what the layers beneath it already define.

| Layer | Answers | Holds | Cites |
|---|---|---|---|
| 4 Evidence | Does it still hold, and can we prove it? | Change log rows, decision records, evaluation sets, audit trail | A rule ID and the version it ran under |
| 3 Rules and contracts | What must the system do? | Decision tables, business rules, API contracts, versioning policy | A glossary term and a data field |
| 2 Shape | What exists, and where does each fact live? | Context diagram, C4 set, data model, sequence diagram | A glossary term and an owner |
| 1 Language | What do the words mean, and who owns what? | Glossary rows, one named owner per requirement, stakeholder map | Nothing below it |

---

## 2. The citation test

Pick one folder and test every item in it. Each item passes when it names something in the layer below.

* A rule row names a glossary term and the entity or field that holds each fact it needs.
* A contract field names the glossary term it carries.
* A diagram box carries a name that matches a glossary row, and an owner.
* A change log row names the rule ID it changed.

An item that cites nothing beneath it means one of two things. The layer below is missing, or the item is guessing. Count the failures per layer. The layer with the most is the one to write next.

---

## 3. What to write when time is short

Match the symptom to the layer.

| Symptom | Layer to write |
|---|---|
| Two teams argue about what a word means | 1 Language |
| Engineers and analysts disagree about where a fact is stored | 2 Shape |
| The same case gets different outcomes depending on who handles it | 3 Rules and contracts |
| A reviewer asks why a rule is what it is, and nobody remembers | 4 Evidence |

Writing a higher layer first is possible. It leaves the top of the pyramid citing words nobody has defined.

---

## 4. Crosswalk to the four levels

The four levels in the Post 50 reference sort a single page by the question it answers. The pyramid orders the work of a team. The two cut across each other, and a document has one of each.

| Layer | Draws on levels | Note |
|---|---|---|
| 1 Language | 1 Intent | Owners and the stakeholder map are Intent. Glossary definitions have no exact home in the levels. The closest is Level 2, since requirements cite them. |
| 2 Shape | 1 Intent, 3 Structure | The context diagram is Intent. C4 diagrams, the data model and sequence diagrams are Structure. |
| 3 Rules and contracts | 2 Behavior, 3 Structure | Business rules and acceptance criteria are Behavior. API contracts are Structure. |
| 4 Evidence | 4 Record | Decision records, change log rows and incident reviews. Evaluation sets and audit trails are records of behavior, so Level 4 is the nearest fit. |

A C4 diagram and an API contract are both Level 3. The diagram sits in layer 2 and the contract in layer 3, because the contract cites what the diagram shows.

---

## 5. Layer as metadata

When documents feed a retriever, the layer and its citations belong in the header next to the level, the status and the review date.

```yaml
level: 3
layer: 3
cites:
  - glossary: settled.ledger_posted
  - entity: PAYMENT_EVENT
status: approved
reviewed: 2026-10-01
```

A retriever that pulls a rule row can follow `cites` down to the definition and the field. A row with no `cites` is a guess the retriever cannot check.

---

## 6. Four rules

**Rule 1: Write bottom-up.** A higher layer is drafted only after the layer below has a definition to cite.

**Rule 2: Every item cites downward.** The citation is part of the document, in the body or in the header.

**Rule 3: The layer is written in the header.** A reader and a retriever both need it without opening the body.

**Rule 4: A failed citation test sends the author down one layer.** The fix goes into the lower document, not into a longer explanation in the upper one.

---

## Related Artifacts

* [artifacts/post-50-four-levels-of-documentation.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-50-four-levels-of-documentation.md) - Sorts a single page by level, which the crosswalk in section 4 sets against the layers
* [artifacts/post-60-cross-functional-glossary.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-60-cross-functional-glossary.csv) - The base layer, with one row per meaning and one owner each
* [artifacts/post-62-er-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-62-er-diagram.md) - A layer 2 artifact that cites the glossary rows
* [artifacts/post-58-decision-table-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-58-decision-table-template.md) - A layer 3 artifact that cites both layers below it
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - Layer 4 rows, each naming the rule it changed

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
