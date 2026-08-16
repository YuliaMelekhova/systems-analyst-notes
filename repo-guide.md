# Repository Guide

**Series:** Systems Analyst Notes  
**Scope:** Repository  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

Says where a file goes in this repository and what it is called. Reach for it before creating any new file, and reach for `anti-ai-artifacts.md` before writing anything inside one.

---

## 0. Which file wins

Three documents govern this repository, and they do not overlap by accident.

| File | Governs | Authority |
|---|---|---|
| `anti-ai-writing.md` | LinkedIn post copy | Wins on voice and phrasing everywhere, including inside artifacts |
| `anti-ai-artifacts.md` | What goes inside an artifact file: header block, body rules, footer, links, phase names, commit messages | Wins on anything about the contents of a file |
| `repo-guide.md`, this file | Repository mechanics: folder layout, naming, file format per content type, weekly workflow | Wins on where a file goes and what it is called |
| `visual-style-guide.md` | The image published with each post | Separate from the repo, listed here so nobody looks for it in the wrong place |

Where this file previously described a header block, it was superseded. That section now points at `anti-ai-artifacts.md` rather than restating it, because two copies of a format rule drift apart and the drift is silent.

This file is itself a repository-level file, which is why it opens with a `Scope: Repository` header block and closes with a footer block, and why it carries no em dashes. A governance document that breaks the rule it is documenting teaches the wrong habit faster than the rule teaches the right one.

The copy of this file kept alongside the writing rules is named `github_repo_guide.md`. In the repository it is `repo-guide.md`. Same content, and the repository name is the one that matters, since that is the copy anyone opens.

---

## 1. Folder structure

```
systems-analyst-notes/
├── README.md                      ← root index (this IS the Post 7 artifact)
├── CONTRIBUTING.md
├── repo-guide.md
├── knowledge-packs/
│   └── README.md                  ← folder index, no header or footer block
├── stride-threat-modeling/
│   └── README.md
├── governance-matrix/
│   └── README.md
├── prompt-library/
│   └── README.md
├── templates-quality-rules/
│   └── README.md
└── artifacts/
    ├── README.md                  ← task-route index, "which file for which job"
    ├── post-10-tribal-knowledge-signs.md
    ├── post-12-knowledge-graph.mmd
    ├── post-14-intake-checklist.md
    ├── post-16-context-diagram.mmd
    ├── post-18-discovery-framework.md
    ├── post-19-unhappy-path-mapping.md
    ├── post-21-requirement-decomposition-template.md
    ├── post-22-api-contract-template.yaml
    ├── post-23-adr-template.yaml
    └── post-24-changelog-template.md
```

Only files that actually exist are listed. An earlier version of this guide carried a projected list of thirty filenames reaching to Post 66, and every one of them was a guess that went stale as the plan moved. The forward-looking list lives in the master plan, in the `GITHUB COMPANION ARTIFACTS` section, which is the one place it can be maintained without duplication.

The five top-level folders mirror the ADF branches from Post 7. They stay mostly empty at first, and they hold branch references rather than post artifacts. `artifacts/` is where the weekly output lands, one file or subfolder per `[GitHub]`-tagged post.

### Four kinds of file live here

`anti-ai-artifacts.md` defines these in full. The short version, because it decides where a file goes:

* **Post artifact.** Lives in `artifacts/`, named `post-NN-slug.ext`, gets a root README row.
* **Branch reference.** Lives in one of the five framework folders, named `descriptive-slug.ext` with no number, gets no root README row. It exists when a topic outlives the post that raised it.
* **Repository-level file.** `README.md`, `CONTRIBUTING.md`, `repo-guide.md`, `artifacts/README.md`. Carries `Scope: Repository`.
* **Folder index.** The `README.md` inside each framework folder. Navigation furniture, no header block, no footer block, and never a list of the files in its own folder.

---

## 2. Naming convention

`post-NN-short-slug.ext`

* `NN` is the two-digit post number, matching the master plan exactly.
* `short-slug` is 2 to 5 words, lowercase, hyphen separated, taken from the post title.
* An inserted post takes the preceding number plus a lowercase letter: `post-28a-mandated-change-register.md`. The plan and the artifact header write it uppercase, `28A`. Sorting holds because `28a` falls between `28` and `29`.
* Multi-file artifacts get a folder rather than a file, same pattern, contents inside without the prefix repeated: `post-48-c4-diagrams/context.mmd`, `container.mmd`, `component.mmd`.

No dates in filenames. The post number is the permanent identifier, and dates live in the README table only.

A number is never reused and never renumbered. Published posts, artifact filenames and README rows all carry it, and none of those can be rewritten after the fact.

---

## 3. File format by artifact type

| Content type | Extension | Example |
|---|---|---|
| Checklists, frameworks, specs, prose docs | `.md` | `post-18-discovery-framework.md` |
| Diagrams (sequence, context, ER, knowledge graph, C4) | `.mmd` Mermaid source | `post-25-sequence-diagram.mmd` |
| Matrices, decision tables, regulatory mappings | `.csv` | `post-53-regulatory-matrix.csv` |
| API contracts, structured records, anything queryable | `.yaml` | `post-22-api-contract-template.yaml` |
| Multi-part artifacts | folder of the above | `post-54-seven-techniques-password-reset/` |

Diagrams go in as Mermaid source rather than exported images. GitHub renders `.mmd` natively in the file preview, and the artifact stays editable instead of becoming a flattened picture.

The `.yaml` row widened after Post 23. A structured record that a rule can validate or a query can reach belongs in YAML even when it reads like prose, because the format is what makes it more than a document. An ADR is the worked example: the same content as markdown can only be read.

A `.csv` file cannot carry a readable footer, so it gets a sibling `post-NN-slug.notes.md` holding the header and footer instead.

---

## 4. Header block

Defined in `anti-ai-artifacts.md`, not here. Open that file before writing one.

Three things worth knowing before you get there, because each has caused a rework:

1. The header is a **visible block**, not an HTML comment. The old comment form documented in this guide has been retired.
2. Every metadata line except the last ends with **two trailing spaces**. Without them the block renders as one paragraph. This fails silently, and only the rendered preview shows it.
3. The phase is written `4 APIs as Products`. Number, space, name. No hyphen, no colon, no dash between them.

The phase itself is taken by counting the section a post sits in inside the master plan. The number range printed in a plan phase heading is a label rather than a source of truth, and it has drifted from the items below it before.

A separate one-line HTML comment above the H1 holds the live post URL. It is added empty at commit time and filled once the post goes live. Post artifacts only.

---

## 5. Root README.md, the index

The root `README.md` is itself the Post 7 artifact. It has two jobs:

1. **State the five-branch structure**: Knowledge Packs, STRIDE Threat Modeling, Governance Matrix, Prompt Library, Templates and Quality Rules. One short paragraph per branch, what lives there conceptually.
2. **List every published artifact** as a table: Post, Title, Phase, Artifact.

Update the table every time a `[GitHub]`-tagged post ships. Nothing else changes, since the five-branch section is written once and stays fixed.

`artifacts/README.md` does a different job and needs its own update when a route changes. The root index answers what the series has published. The artifacts index answers which file to open for the task in hand.

The folder name `templates-quality-rules/` uses a hyphen because folder names cannot carry spaces. Everywhere the branch is named in prose, in a header, or in the root README, it is written `Templates and Quality Rules` with the word.

---

## 6. Weekly workflow

1. A post tagged `[GitHub]` in the master plan has a companion artifact.
2. Draft the post copy. Check it against the 3,000 character LinkedIn limit before the artifact work starts, because a post that has to lose a section may move that section to a different post, and the artifact follows the section.
3. Build the artifact using the format table above and the rules in `anti-ai-artifacts.md`.
4. Build the image using `visual-style-guide.md`, then open it and look at it. Matplotlib clips nothing and warns about nothing.
5. Drop the artifact in `artifacts/`, named per the convention.
6. Add one row to the root README table, and a route to `artifacts/README.md` if the file changes one.
7. Add reverse links in any older artifact that should now point forward, in the same commit.
8. Commit straight to `main`, message form per `anti-ai-artifacts.md`.
9. Add the repo link to the LinkedIn post before it is scheduled, then fill the traceability comment in the artifact once the post is live.

No branches, no pull requests. This is a single-contributor reference repo.

Step 9 is the one that gets forgotten, because it happens after the satisfying part is done. An artifact with an empty `<!-- LinkedIn: -->` comment three weeks after publication is the normal failure here.

---

## Related Artifacts

* [README.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/README.md) - The published index, and the row you add in step 6
* [artifacts/README.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/README.md) - The task-route index, updated when a file changes which route someone would take
* [CONTRIBUTING.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/CONTRIBUTING.md) - What earns an artifact in the first place, before any of the mechanics here apply

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
