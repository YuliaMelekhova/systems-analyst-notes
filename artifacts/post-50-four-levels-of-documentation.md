<!-- LinkedIn: -->

# Four Levels of Documentation

**Series:** Systems Analyst Notes  
**Post:** 50  
**Phase:** 6 AI Agents at Work  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Sorts any document into one of four levels by the question it answers, so each one gets the right reader, owner and review trigger. Reach for it when a document has started answering two questions at once, or before deciding where a new page should live.

---

## 1. The four levels

| Level | Answers | Typical artifacts | Primary reader |
|---|---|---|---|
| 1 Intent | Why does this exist? | Goal and success metric, scope and boundary, context diagram, stakeholder map | Sponsor, new hire |
| 2 Behavior | What must it do, and what happens when it fails? | Requirements, acceptance criteria, unhappy paths, business rules | Product owner, testers |
| 3 Structure | How is it built, and how do the parts talk? | C4 diagrams, API contracts, sequence diagrams, data model, runbooks | Engineers, agents |
| 4 Record | What changed, and why? | Decision records, change log rows, versioning notices, incident reviews | Anyone, months later |

---

## 2. Lifespan, review and what breaks

| Level | Changes when | Review trigger | What breaks when it is missing |
|---|---|---|---|
| 1 Intent | Strategy shifts | Strategy review | Features nobody can justify, and priority arguments with no shared goal |
| 2 Behavior | A feature is scoped or changed | Each release | Acceptance by feeling, and unhappy paths found in production |
| 3 Structure | The code or a contract changes | Each merge | Nobody can see what a change touches, for people or for agents |
| 4 Record | Something changes or happens | None, it is only appended to | The reason is lost, and it cannot be rebuilt because it lived in someone's head |

Level 3 goes stale fastest and has the most readers who act on it. Level 4 is the one most teams skip.

---

## 3. Placement test

Ask four questions of any document. Each yes points to a level.

* Does it explain why this thing exists or who it is for? Level 1.
* Does it say what the system must do, or what happens when something fails? Level 2.
* Does it describe how parts are built or how they talk to each other? Level 3.
* Does it say what changed, when, and why? Level 4.

One yes means the document is placed. Two or more yeses mean it is mixed, and it gets split.

---

## 4. Four rules

**Rule 1: One document belongs to one level.** A section from another level becomes its own page with a link.

**Rule 2: The level is written in the header.** A reader and a retriever both need to know without reading the body.

**Rule 3: Every document links up and down.** Up to the intent it serves, down to the design that implements it. A requirement with no link up is unjustified. A design with no link up is unrequested.

**Rule 4: A page that cannot name its level is split before anyone writes another paragraph.** The page is usually two documents that grew into one file.

---

## 5. Symptoms of a mixed document

| Symptom | Levels mixed | Split into |
|---|---|---|
| Business case on page 2, field list on page 19 | 1 and 3 | An intent page and a contract |
| Requirement ticket with design decisions buried in the comments | 2 and 4 | The requirement, and a decision record |
| README that holds a runbook and a project history | 3 and 4 | A runbook, and a change log |
| Spec where the retry policy was rewritten twice and nobody can say when | 3 and 4 | The current policy, and dated change log rows |

---

## 6. Level as metadata

When documents feed a retriever, the level belongs in the metadata next to status and date. A Level 3 page not reviewed in months is a suspect. A Level 1 page from last year usually is not. Set the staleness threshold per level instead of one threshold for the whole wiki.

```yaml
level: 3
topic: payment-orchestrator
owner: payments-platform
status: approved
reviewed: 2026-10-01
```

---

## 7. The payment platform mapped to the four levels

| Level | Artifact |
|---|---|
| 1 Intent | [artifacts/post-16-context-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.md) |
| 1 Intent | [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) |
| 2 Behavior | [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) |
| 2 Behavior | [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) |
| 3 Structure | [artifacts/post-49-c4-diagrams/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/artifacts/post-49-c4-diagrams/) |
| 3 Structure | [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) |
| 3 Structure | [artifacts/post-25-sequence-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.md) |
| 3 Structure | [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) |
| 4 Record | [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) |
| 4 Record | [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) |
| 4 Record | [artifacts/post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) |

---

## Related Artifacts

* [artifacts/post-49-c4-diagrams/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/artifacts/post-49-c4-diagrams/) - Level 3 in practice: one platform drawn at three zoom levels
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - The row format that fills Level 4
* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - Level 4 decision records as structured data
* [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) - Produces the Level 1 and Level 2 documents

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
