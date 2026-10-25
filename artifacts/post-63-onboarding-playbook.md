<!-- LinkedIn: -->

# AI-Assisted Onboarding Playbook

**Series:** Systems Analyst Notes  
**Post:** 63  
**Phase:** 8 Scaling  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Sets the shape of an onboarding plan for new analysts who work next to an AI-assisted knowledge base, with the assistant's settings and an unaided checkpoint at every stage. Reach for it before the first new hire gets access to the assistant.

---

## 1. Why it measures two things

A knowledge base earns its keep on containment: the share of routine questions answered without a senior colleague's time. That number says nothing about whether the new analyst can reason through an ambiguous requirement alone, so the playbook reports it next to an unaided checkpoint.

A field experiment published in PNAS in 2025 gives the mechanism a measured shape. Nearly a thousand high school math students practiced with a GPT-4 tutor. Those with a plain chat assistant scored 48% higher on practice problems, then 17% lower than a no-AI group on the exam once the assistant was removed. Most of them had asked for the answer. A second group used the same assistant set to give hints and loaded with common student mistakes. They scored 127% higher in practice, and their exam results matched the no-AI group.

The study covered one school and one subject. Treat it as a mechanism to test on your own team, not as a result to cite.

---

## 2. Values you set once

Four values are decided once and appear throughout. The starting values are a place to begin, not a finding.

| Value | Written as | Starting value |
|---|---|---|
| Number of tickets worked by hand | `[HAND_TICKETS]` | 3 |
| Knowledge base owner | `[KB_OWNER]` | The senior analyst who maintains the knowledge base |
| Checkpoint reviewer | `[REVIEWER]` | A senior analyst who is not the new hire's daily mentor |
| Report period | `[REPORT_PERIOD]` | Monthly |

---

## 3. Chapter 1: Map

The map says what the knowledge base holds and which questions it refuses. A new hire who knows the refusals stops treating a missing answer as a failure.

| Field | What to write |
|---|---|
| Sources held | Each source type, its owner and its review date |
| Questions it answers | Lookups with a written source: where a decision is recorded, which rule applies, who owns a service |
| Questions it refuses | Anything that needs judgment, and anything whose source is missing or out of date |
| Owner | `[KB_OWNER]`, named, with a date for the next review of the map |

---

## 4. Chapter 2: On-ramp

Four stages. The assistant mode changes at each one, and a stage ends only when the checkpoint in chapter 4 is passed.

| Stage | Length | Assistant mode | Work |
|---|---|---|---|
| 1 Orientation | Week 1 | Locate | Read, and ask where things are. Find the decision record behind three live requirements. |
| 2 Hand-worked tickets | Until `[HAND_TICKETS]` tickets are done | Locate | The analyst writes every word. The assistant finds and links sources only. |
| 3 Hint first | About 3 weeks | Hint | The analyst drafts. The assistant shows precedent, asks a guiding question and points at gaps. |
| 4 Draft on request | From then on | Draft | The analyst writes an outline first. The assistant may write a first draft and lists its assumptions. |

Stage 2 only works if each hand-worked ticket has a precedent in the knowledge base. Choose the tickets in advance.

---

## 5. Chapter 3: Assistant settings

One row per mode. The instruction line goes into the assistant's configuration, and the "may not" column is tested before the first hire starts.

| Mode | May do | May not do | Instruction line |
|---|---|---|---|
| Locate | Find and link sources, name the owner of a page | Summarize a decision as a conclusion, write requirement text | Point to the source and stop. |
| Hint | Show a precedent, ask one guiding question, flag a gap in the analyst's draft, name a common mistake | Write requirement text, give the answer when asked directly | Ask a question that leads to the precedent. Do not complete the task. |
| Draft | Write a first draft from the analyst's outline, list every assumption it made | Skip the assumptions list, change the outline without saying so | Draft from the outline and flag what you assumed. |

### The common mistakes list

The assistant loads a short file of mistakes seen in review, so it can recognize an error without inventing one. Four starting entries:

| Mistake | How it shows up |
|---|---|
| The requirement stops at "integration completed" | No customer outcome in the acceptance criteria |
| A rule written with a word that has several meanings | The glossary has more than one row for the term |
| Only the happy path is written | No failure behavior, no needs-review case |
| A retry with no stop condition | No maximum attempts, no escalation path |

Add an entry each time a senior analyst corrects the same thing twice.

---

## 6. Chapter 4: Checkpoint

One unaided task at the end of each stage. The new hire works with the assistant switched off, and `[REVIEWER]` reviews the result against a written rubric.

| Stage | Unaided task | The reviewer asks |
|---|---|---|
| 1 | Find the decision record behind one live requirement and explain why that option won | Could they find it, and could they say what the rejected options were? |
| 2 | Turn a raw request into a requirement with acceptance criteria and two failure paths | Would the criteria be testable by someone who never met the requester? |
| 3 | Review a colleague's requirement and name what evidence would change the reading | Did they go to a source, or ask for agreement? |
| 4 | Take an ambiguous request to an outline, with assumptions listed | Is every assumption written down and owned? |

The reviewer records pass or revisit, plus one sentence on what the analyst missed.

---

## 7. Reading the two measures together

Containment comes from the knowledge base logs. The checkpoint result comes from chapter 4. Read them as a pair every `[REPORT_PERIOD]`.

| Containment | Checkpoints | What it usually means | Action |
|---|---|---|---|
| High | Passing | The setup works | Keep going |
| High | Failing | The assistant is doing the work | Move the new hire back one stage |
| Low | Passing | The knowledge base has gaps | Fix the map and the sources |
| Low | Failing | The onboarding itself is thin | Review chapters 1 and 2 |

---

## 8. Review gate

Four checks before the first new hire starts. The second is the one that catches a misconfigured assistant.

1. Does every source in the map have an owner and a review date?
2. Has each assistant mode been tested with a direct request for the answer, and does Hint mode decline and ask a question instead?
3. Are the hand-worked tickets chosen, each with a precedent the new hire can find?
4. Is the checkpoint reviewer named, and is the rubric written?

---

## Related Artifacts

* [artifacts/post-34-knowledge-pack-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-34-knowledge-pack-template.md) - The shape of the entries the map chapter lists
* [artifacts/post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md) - The fields the assistant needs on record before it is configured
* [artifacts/post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md) - The threshold thinking behind a pass or revisit at each checkpoint
* [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) - Why a reviewer needs training before a checkpoint counts as a control

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
