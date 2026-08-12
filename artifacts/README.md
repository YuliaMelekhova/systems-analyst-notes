# Artifacts Index

Series: Systems Analyst Notes
Scope: Repository
Author: Yulia Melekhova
Published: 2026

## Purpose

The same files the root README lists, grouped by what they do instead of by post number. Reach for it when looking for a kind of artifact rather than a specific post.

---

## By Task

Most people arrive here mid-task. This section answers the question that brought them.

**About to write a requirement.** Start with [post-14-intake-checklist.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-14-intake-checklist.md), which decides whether writing it now is worth the time. Then [post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) for the discovery pass that produces the content.

**Requirement drafted, unsure what is missing.** [post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) surfaces the failure behavior, and [templates-quality-rules/requirement-antipatterns.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/requirement-antipatterns.md) covers the gaps that survive a normal review.

**Scoping a system boundary.** [post-16-context-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.md) comes first, and the trust boundaries in [stride-threat-modeling/payment-initiation-stride.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/stride-threat-modeling/payment-initiation-stride.md) are drawn on top of it.

**Inheriting an undocumented system.** [post-10-tribal-knowledge-signs.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-10-tribal-knowledge-signs.md) for where the risk sits, then [post-12-knowledge-graph.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-12-knowledge-graph.md) for mapping what connects to what.

**Preparing a review process.** [templates-quality-rules/readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) holds the gates and the status model.

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

### Diagrams

Mermaid source, editable rather than exported.

| Artifact | What it shows |
|---|---|
| [post-12-knowledge-graph.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-12-knowledge-graph.md) | How documentation nodes connect, and where the orphans are |
| [post-16-context-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.md) | A system boundary with its external actors |

---

## The Other Folders

`artifacts/` holds files tied to a numbered post. The five framework folders hold standing references that outlive any single post and get updated as standards move.

* [knowledge-packs/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/knowledge-packs/) - Standards and domain reference, written once and reused
* [stride-threat-modeling/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/stride-threat-modeling/) - Threat models cross-linked to the requirements they change
* [governance-matrix/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/governance-matrix/) - Which regulatory framework reaches which market
* [prompt-library/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/prompt-library/) - Analytical prompts kept as reusable references
* [templates-quality-rules/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/templates-quality-rules/) - Artifact templates plus the rules that decide when one is ready

---

## Related Artifacts

* [CONTRIBUTING.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/CONTRIBUTING.md) - The test every file here passed before it was committed
* [repo-guide.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/repo-guide.md) - Naming, header and footer conventions used across the repository

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
