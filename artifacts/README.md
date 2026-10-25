# Artifacts Index

**Series:** Systems Analyst Notes  
**Scope:** Repository  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

The same files the root README lists, plus the standing references in the five framework folders, grouped by what they do instead of by post number. Reach for it when looking for a kind of artifact rather than a specific post.

---

## By Task

Most people arrive here mid-task. This section answers the question that brought them.

**About to write a requirement.** Start with [post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md), which decides whether writing it now is worth the time. Then [post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) for the discovery pass that produces the content.

**Requirement drafted, unsure what is missing.** [post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) surfaces the failure behavior, and [templates-quality-rules/requirement-antipatterns.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/requirement-antipatterns.md) covers the gaps that survive a normal review.

**Scoping a system boundary.** [post-16-context-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.md) comes first, and the trust boundaries in [stride-threat-modeling/payment-initiation-stride.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/stride-threat-modeling/payment-initiation-stride.md) are drawn on top of it.

**Inheriting an undocumented system.** [post-10-tribal-knowledge-signs.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-10-tribal-knowledge-signs.md) for where the risk sits, then [post-12-knowledge-graph.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-12-knowledge-graph.md) for mapping what connects to what.

**Preparing a review process.** [templates-quality-rules/readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) holds the gates and the status model.

**Tracking a regulatory deadline you don't control.** [post-29-mandated-change-register.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-29-mandated-change-register.csv) holds one row per obligation, classified as breaking or non-breaking against the policy in [post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md).

**Breaking down a requirement that spans services.** [post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) names the services, owners and contracts touched. [post-25-sequence-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.md) draws the conversation between them, and [post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) fixes what each arrow is allowed to send.

**Changing a published API.** [post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) decides whether the change is breaking and what notice the client gets. [post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) records what changed and why.

**Recording why a decision was made.** [post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) keeps the decision in structured form, with the merge gate that stops a record shipping half-filled.

**Turning a meeting or a document into a knowledge base entry.** [post-34-knowledge-pack-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-34-knowledge-pack-template.md) sets the shape and the required metadata. [cross-border-payments-glossary.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/cross-border-payments-glossary.md) covers the payment terms that mean different things to different reviewers.

**Onboarding a new analyst next to an AI assistant.** [post-63-onboarding-playbook.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-63-onboarding-playbook.md) sets four stages, the assistant's settings per stage and an unaided checkpoint.

**Specifying a payment flow.** [iso-20022-cbpr-plus.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/iso-20022-cbpr-plus.md) covers what the November 14, 2026 address requirement changes in the data model and the API contract. [payment-initiation-stride.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/stride-threat-modeling/payment-initiation-stride.md) is a worked threat pass over one flow, to copy as a shape.

**Putting an AI agent into production.** Start with [post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md) for the seven fields and the pre-launch checklist. Then [post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md) sets the shipping threshold per task type, and [post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) places the human checkpoints and the kill switch.

**Designing a multi-step agent pipeline.** [post-47-automation-pipeline-map.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-47-automation-pipeline-map.md) draws the coordinator and the specialist steps, and [post-48-loop-engineering-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-48-loop-engineering-spec.md) sets the stop conditions and restart rules for each step.

**Deciding where a document belongs.** [post-50-four-levels-of-documentation.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-50-four-levels-of-documentation.md) sorts it by the question it answers, which also decides its owner and review trigger.

**Deciding what to document first.** [post-64-documentation-pyramid.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-64-documentation-pyramid.md) orders four layers from shared language up to evidence, and its citation test shows which layer is thin. [post-50-four-levels-of-documentation.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-50-four-levels-of-documentation.md) then places each page.

**Documenting one requirement for several audiences.** [post-56-seven-techniques-password-reset/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/artifacts/post-56-seven-techniques-password-reset/) writes the same requirement seven ways, one per reader.

**Finding where each fact a rule needs is stored.** [post-62-er-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-62-er-diagram.md) gives eight entities and the questions to settle before build. A rule row from [post-58-decision-table-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-58-decision-table-template.md) points at the box that holds its facts.

**Letting an assistant answer from a written policy.** [post-58-decision-table-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-58-decision-table-template.md) turns each rule into a row with a condition, an evidence source, an outcome and an owner. Missing evidence returns needs_review instead of a guess, so application code decides and the model only explains.

**Two teams use the same word differently.** [post-60-cross-functional-glossary.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-60-cross-functional-glossary.csv) holds one row per meaning of a shared word, each with its own name, owner and the rows it conflicts with. Read its [notes file](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-60-cross-functional-glossary.notes.md) first for the review gate. [cross-border-payments-glossary.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/cross-border-payments-glossary.md) covers payment terms that are ambiguous across standards and markets, so check it before adding a row.

**Finding which rules reach a market.** [market-framework-matrix.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/governance-matrix/market-framework-matrix.csv) starts from the market and lists the frameworks that apply, and where two of them disagree. Read its notes file first.

**Justifying one AI control to several regulators.** [ai-regulatory-control-matrix.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/governance-matrix/ai-regulatory-control-matrix.csv) starts from the control and lists the provisions it answers to, so one piece of evidence can be cited more than once.

---

## By Type

### Checklists and diagnostics

Files that produce a verdict on something that already exists.

| Artifact | What it decides |
|---|---|
| [post-10-tribal-knowledge-signs.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-10-tribal-knowledge-signs.md) | Whether undocumented knowledge has become an operational risk |
| [post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md) | Whether a requirement is ready to be written at all |

### Frameworks and methods

Files that describe a sequence to run.

| Artifact | What it produces |
|---|---|
| [post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) | A discovery pass with entry and exit criteria per step |
| [post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) | Specified behavior for the paths that are not the happy one |
| [post-50-four-levels-of-documentation.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-50-four-levels-of-documentation.md) | A level, a reader, an owner and a review trigger for any document |
| [post-63-onboarding-playbook.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-63-onboarding-playbook.md) | Four onboarding stages, each with assistant settings and an unaided checkpoint |
| [post-64-documentation-pyramid.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-64-documentation-pyramid.md) | A build order for documentation, with a citation test per layer |

### Templates

Files with a fixed shape to copy and fill in. The two YAML files are structured on purpose, so a rule can validate them and a query can reach them.

| Artifact | What it gives you |
|---|---|
| [post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) | The services, owners and contracts one requirement touches |
| [post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) | An API contract skeleton with the analyst-relevant fields flagged |
| [post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) | A structured decision record with a merge gate |
| [post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) | Five columns that record what changed in a requirement and why |
| [post-34-knowledge-pack-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-34-knowledge-pack-template.md) | A Knowledge Pack built from a raw source, with the metadata retrieval needs |
| [post-56-seven-techniques-password-reset/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/artifacts/post-56-seven-techniques-password-reset/) | One requirement written seven ways, with the maintenance rule that keeps them in step |
| [post-58-decision-table-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-58-decision-table-template.md) | A rule table where every rule has a condition, an evidence source and an outcome, with needs review as a third result |

### Policies and registers

Files that settle a rule once, or track rows that change over time.

| Artifact | What it settles or tracks |
|---|---|
| [post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) | What counts as a breaking change, and the notice a client gets |
| [post-29-mandated-change-register.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-29-mandated-change-register.csv) | Regulatory obligations that change an API on someone else's schedule |
| [post-60-cross-functional-glossary.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-60-cross-functional-glossary.csv) | Which meaning of a shared word each team uses, with one owner per meaning |

### Agent specifications

Files that fix what an AI agent needs on record before anyone builds it.

| Artifact | What it fixes |
|---|---|
| [post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md) | The seven fields every agent needs on record, with a pre-launch checklist |
| [post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) | Five checkpoint tiers and a kill switch, each with the control that enforces it |
| [post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md) | The shipping threshold, review policy and owner per task type |
| [post-47-automation-pipeline-map.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-47-automation-pipeline-map.md) | The coordinator and specialist shape, five infrastructure layers and the cache technique |
| [post-48-loop-engineering-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-48-loop-engineering-spec.md) | Stop conditions, risk tier and restart rules for each pipeline step |

### Diagrams

Mermaid source, editable rather than exported.

| Artifact | What it shows |
|---|---|
| [post-12-knowledge-graph.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-12-knowledge-graph.md) | How documentation nodes connect, and where the orphans are |
| [post-16-context-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.md) | A system boundary with its external actors |
| [post-25-sequence-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.md) | One payment as a timed conversation between services, with the branches and retries |
| [post-49-c4-diagrams/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/artifacts/post-49-c4-diagrams/) | A payment platform at context, container and component level |
| [post-62-er-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-62-er-diagram.md) | The data behind a payment platform's rules, with the cardinality each line commits to |

---

## Standing References

`artifacts/` holds files tied to a numbered post. The five framework folders hold references that outlive any single post and get updated as standards move, so they carry no post number.

| Branch | File | Reach for it when |
|---|---|---|
| Knowledge Packs | [iso-20022-cbpr-plus.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/iso-20022-cbpr-plus.md) | Scoping a payment initiation flow, or deciding how much of the address structure to build now |
| Knowledge Packs | [cross-border-payments-glossary.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/cross-border-payments-glossary.md) | A requirement uses a payment term and the reviewers appear to agree on what it means |
| STRIDE Threat Modeling | [payment-initiation-stride.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/stride-threat-modeling/payment-initiation-stride.md) | Threat modeling a payment flow and a worked shape is easier to copy than a control list |
| Governance Matrix | [market-framework-matrix.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/governance-matrix/market-framework-matrix.csv) and [notes](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/governance-matrix/market-framework-matrix.notes.md) | Finding which framework reaches which market, and where two that both apply disagree |
| Governance Matrix | [ai-regulatory-control-matrix.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/governance-matrix/ai-regulatory-control-matrix.csv) and [notes](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/governance-matrix/ai-regulatory-control-matrix.notes.md) | Justifying one AI control to several regulators, or checking what a new market already covers |
| Templates and Quality Rules | [readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) | A review cycle keeps producing the same corrections, or nobody can say whether a draft is finished |
| Templates and Quality Rules | [requirement-antipatterns.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/requirement-antipatterns.md) | A review pass, or an incident traced back to a document everyone had approved |

The two Governance Matrix files answer different questions. The market matrix starts from a market and lists the frameworks that reach it. The control matrix starts from an architecture control and lists the provisions it answers to.

The five folders themselves:

- [knowledge-packs/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/knowledge-packs/) - Standards and domain reference, written once and reused
- [stride-threat-modeling/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/stride-threat-modeling/) - Threat models cross-linked to the requirements they change
- [governance-matrix/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/governance-matrix/) - Which regulatory framework reaches which market, and which provisions each AI control answers to
- [prompt-library/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/prompt-library/) - Analytical prompts kept as reusable references
- [templates-quality-rules/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/templates-quality-rules/) - Artifact templates plus the rules that decide when one is ready

---

## Related Artifacts

* [CONTRIBUTING.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/CONTRIBUTING.md) - The test every file here passed before it was committed
* [repo-guide.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/repo-guide.md) - Naming, header and footer conventions used across the repository

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
