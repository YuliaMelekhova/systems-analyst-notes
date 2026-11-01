<!-- LinkedIn: -->

# Systems Analysis Function Build Map

**Series:** Systems Analyst Notes  
**Post:** 67  
**Phase:** 9 Reflection  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

Orders the artifacts in this repository into six stages for a team building a systems analysis function from nothing, with a test a stranger can run to say whether each stage stands. Reach for it when the question is which file to build next, rather than which file fits a task.

---

## 1. What this file is not

Two indexes already exist. The root [README.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/README.md) lists what the series has published. [artifacts/README.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/README.md) answers which file to open for the task in hand. This file answers a third question: what a team builds next, in what order, and how it knows the stage is done.

---

## 2. What counts as a function

One analyst produces documents. A function exists when five questions can be answered from files, without finding the person who knows. A sixth question applies once an AI agent reads those files.

The check is the same at every stage. Hand someone who did not write the files the stage's question and the folder. If they can answer from the files alone, the stage stands. If the answer needs a message to a person, that message is the gap, and it becomes the next row to write.

**Before stage 1.** Run [artifacts/post-10-tribal-knowledge-signs.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-10-tribal-knowledge-signs.md) to see how much of the knowledge lives only in someone's head. Use [artifacts/post-12-knowledge-graph.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-12-knowledge-graph.md) to map what connects to what. This decides where to start and does not count as a stage.

---

## 3. The six stages

Each stage cites the one before it. A rule row names a glossary term and the field that holds each fact it needs. A contract field names the term it carries. Build in this order and each stage has something to cite.

| Stage | The question | Files | Exit test |
|---|---|---|---|
| 1 Language | What do the words mean, and who owns what? | [artifacts/post-60-cross-functional-glossary.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-60-cross-functional-glossary.csv), [knowledge-packs/cross-border-payments-glossary.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/cross-border-payments-glossary.md) | Take five terms from the last five requirements. Each has one row per meaning and one named owner, and the requirement says which meaning it uses. |
| 2 Intake | Is this request ready to be written? | [artifacts/post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md), [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md), [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md), [templates-quality-rules/readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) | Take the last three requirements that reached review. Each shows an intake result, and none would have been returned unread under the readiness rules. |
| 3 Shape | What does it touch? | [artifacts/post-16-context-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.md), [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md), [artifacts/post-25-sequence-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.md), [artifacts/post-49-c4-diagrams/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/artifacts/post-49-c4-diagrams/), [artifacts/post-62-er-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-62-er-diagram.md) | Take one requirement. The files name every service it touches, each service's owner, and where each fact it needs is stored. |
| 4 Rules | What must it do, and when is it wrong? | [artifacts/post-58-decision-table-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-58-decision-table-template.md), [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml), [artifacts/post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md), [artifacts/post-29-mandated-change-register.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-29-mandated-change-register.csv) | Take one rule. Its row states the condition, the evidence source, the outcome, the owner and a needs-review case. Its contract field names the glossary term it carries. |
| 5 Record | What changed, and why? | [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml), [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) | Take one value that changed last quarter. A row says what changed, why, who asked and what else moved. |
| 6 Agents | Can a machine act on this safely? | [artifacts/post-34-knowledge-pack-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-34-knowledge-pack-template.md), [artifacts/post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md), [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md), [artifacts/post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md), [artifacts/post-47-automation-pipeline-map.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-47-automation-pipeline-map.md), [artifacts/post-48-loop-engineering-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-48-loop-engineering-spec.md) | For the folder the agent reads, stages 1 to 5 pass their tests, and the agent has a named owner, a written threshold and a human checkpoint. |

A stage that fails its test sends the author back one stage. The fix goes into the lower stage, not into a longer explanation in the higher one.

---

## 4. The record starts early

Stages are ordered by what each one cites. Stage 5 is the exception, because it cannot wait for its turn. The reason a limit is 5 and not 3 lives in someone's head until the day it is written, and after that it cannot be rebuilt. Start the change log the day the first requirement is approved, and add decision records as decisions are made, while stages 1 to 4 are still being built.

---

## 5. Before an agent reads a folder

Four checks, run on the folder and not on the agent.

1. Does every term the pages use have one meaning, with an owner? An agent given a word with three meanings picks one silently.
2. Does every page carry a status and a version? Without them an agent cannot tell a current page from a superseded one.
3. Does every page have a named owner, so a wrong answer has somewhere to go?
4. Does the change log show recent activity where the requirements changed? A log with no rows in a month of changes means the pages are older than they look.

---

## 6. Four numbers from the first month

| Number | How to count it | What it shows |
|---|---|---|
| Lead time | Days from a request landing to a requirement a developer can build from. Fix where the clock starts and stops before measuring, and log the days spent waiting for an answer from a person | Where the days go: writing, or waiting |
| Questions that reach a person | Questions per week answered by messaging a named person where a file should have answered. Keep a tally in a shared note | Which stage is thin. Each tally is a candidate gap |
| Change log rows added | Rows added per month, set against the number of approved changes in the same month | Whether the log is used or only exists |
| Pages with a named owner and a status | The share of pages that carry both | The ownerless pages, which are the actual problem underneath most documentation debt |

---

## 7. Where the ordering comes from

The stage order applies the layer logic in [artifacts/post-64-documentation-pyramid.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-64-documentation-pyramid.md) to a whole function. To place a single page once it exists, use [artifacts/post-50-four-levels-of-documentation.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-50-four-levels-of-documentation.md). The pyramid orders the work, and the four levels sort the pages.

---

## Related Artifacts

* [artifacts/post-64-documentation-pyramid.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-64-documentation-pyramid.md) - The write-bottom-up rule this map applies across stages, with a citation test per layer
* [artifacts/post-50-four-levels-of-documentation.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-50-four-levels-of-documentation.md) - Places any single page once it exists, which stage 3 and stage 4 files need
* [artifacts/README.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/README.md) - The task-route index, for when the question is which file fits the job in hand
* [artifacts/post-63-onboarding-playbook.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-63-onboarding-playbook.md) - What a new analyst does inside these stages, with an unaided checkpoint at each one
* [artifacts/post-10-tribal-knowledge-signs.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-10-tribal-knowledge-signs.md) - The diagnosis that decides which stage to start with

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
