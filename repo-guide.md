# Repository Guide

**Series:** Systems Analyst Notes  
**Scope:** Repository  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

The mechanical conventions every file here follows: folder structure, naming, header and footer blocks, formats and link style. Reach for it before adding a file, or when copying this structure for a documentation set elsewhere.

---

## Structure

```
systems-analyst-notes/
├── README.md                  index and five-branch overview
├── CONTRIBUTING.md            what gets in and what does not
├── repo-guide.md              this file
├── artifacts/                 one file per numbered post
│   └── README.md              index grouped by type and by task
├── knowledge-packs/
├── stride-threat-modeling/
├── governance-matrix/
├── prompt-library/
└── templates-quality-rules/
```

The five framework folders mirror the branches of the documentation framework described in the root README. `artifacts/` holds companion files for numbered posts in the series.

---

## Two Kinds of File

The distinction drives the header block, the naming rule and whether a root README row is needed.

| | Post artifact | Branch reference |
|---|---|---|
| Lives in | `artifacts/` | One of the five framework folders |
| Named | `post-NN-slug.ext` | `descriptive-slug.ext` |
| Header carries | `Post` and `Phase` | `Branch` |
| Root README row | Yes | No |
| Changes after publication | Corrections only | Updated as standards move |

Repository-level files at the root use `Scope: Repository` in place of both, and follow the branch reference rules otherwise.

---

## Naming

Post artifacts: `post-NN-short-slug.ext`

* `NN` is the two-digit post number and is the permanent identifier.
* `short-slug` is two to five words, lowercase, hyphen separated, drawn from the post title.
* Multi-file artifacts get a folder with the same prefix, and the contents drop the prefix. For example `post-41-c4-diagrams/context.mmd`.

Branch references: a descriptive slug with no number, since they are not tied to a post.

No dates in file names, in either kind. Dates live in the README table and in the verification note inside a file.

---

## Format by Content Type

| Content | Extension |
|---|---|
| Checklists, frameworks, specs, prose | `.md` |
| Diagrams | `.mmd`, or a fenced Mermaid block inside a `.md` file |
| Matrices, decision tables, regulatory mappings | `.csv` |
| API contract skeletons | `.yaml` |
| Multi-part artifacts | A folder of the above |

Diagrams ship as source rather than exported images, which keeps them editable and lets GitHub render them.

One rendering detail worth knowing: GitHub renders Mermaid inside fenced code blocks in `.md` files reliably. A standalone `.mmd` file does not always preview. Where the diagram is the artifact and the preview matters, a `.md` wrapper is the safer choice. Inside the Mermaid source, `\n` in node labels and `direction TB` inside a subgraph both break rendering.

---

## Header Block

First thing in the file, plain text, no badges.

Post artifact:

```markdown
# Unhappy Path Mapping Framework

**Series:** Systems Analyst Notes  
**Post:** 19  
**Phase:** 3 Building the Foundation  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

One or two sentences on what this artifact does and when to reach for it.
```

Branch reference:

```markdown
# ISO 20022 CBPR+ Structured Address Knowledge Pack

**Series:** Systems Analyst Notes  
**Branch:** Knowledge Packs  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

One or two sentences on what this artifact does and when to reach for it.
```

`Purpose` states what someone does with the file. It is not a summary of the post.

### The header renders line by line

Each metadata line ends with **two trailing spaces**. That is the Markdown hard line break. Without it, consecutive lines collapse into one paragraph and the header renders as a single run of text.

```
**Series:** Systems Analyst Notes··
**Post:** 19··
**Phase:** 3 Building the Foundation··
**Author:** Yulia Melekhova··
**Published:** 2026
```

The `·` marks stand for spaces and are not typed. The last line takes no trailing spaces, since a blank line follows it anyway.

Field labels are bold, values are plain. A single newline is not enough on its own, and this is the one formatting rule in the repository that fails silently: the file looks correct in an editor and renders wrong on GitHub.

Trailing whitespace is invisible, and some editors strip it on save. Check the rendered preview before committing rather than trusting the source view.

Post artifacts carry one HTML comment above the H1 holding the live post URL, added empty at commit and filled once the post is live:

```markdown
<!-- LinkedIn: https://www.linkedin.com/posts/... -->
```

Branch references have no post to link and skip the comment.

`.yaml` and `.mmd` carry the same header in their own comment syntax, `#` and `%%`. A `.csv` gets a sibling `slug.notes.md` holding the header and footer, since links inside a CSV are unreadable.

---

## Phase Names

One canonical form everywhere. Number, space, name. No hyphen, no colon between the number and the name.

* Phase 1 Arrival: Where Is the Truth?
* Phase 2 The Knowledge Chapter
* Phase 3 Building the Foundation
* Phase 4 APIs as Products
* Phase 5 Bringing AI Into the Workflow
* Phase 6 AI Agents at Work
* Phase 7 Process, Compliance and Fintech Reality
* Phase 8 Scaling
* Phase 9 Reflection
* Phase 10 New Additions

The colon inside `Phase 1 Arrival: Where Is the Truth?` belongs to the phase title and stays.

---

## Footer Block

Last thing in the file, after a horizontal rule.

```markdown
---

## Related Artifacts

* [artifacts/post-18-discovery-framework.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-18-discovery-framework.md) - Step 4 covers unhappy path discovery

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
```

Four rules govern it:

1. `Related Artifacts` appears only when at least one relation exists. With none, the two sign-off lines stand alone.
2. Each entry is a link, a space, a plain hyphen, a space, and one clause giving a reason to click. Not a description of the file.
3. Relations are ordered by relevance, not by post number.
4. When a relation is symmetric, the older file gets the reverse link in the same commit. One-directional links decay, because the person editing the older file never sees the newer one.

---

## Link Format

One canonical form, used in files and in both READMEs. Link text is the repository-relative path, link target is the absolute URL, and both point at the same file.

```
[artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md)
```

Folders use `tree` in place of `blob`:

```
[knowledge-packs/](https://github.com/YuliaMelekhova/systems-analyst-notes/tree/main/knowledge-packs/)
```

The recurring error is a doubled `artifacts/artifacts/` in the URL. Every link is checked before commit.

---

## Writing Rules

Applied to every file, including the READMEs.

**No em dashes.** An en dash only where a dash carries real meaning. Splitting the sentence in two is almost always better. Plain hyphens in file names, compound words and related-artifact bullets are hyphens and are fine.

**Step headers use colons.** `Step 1: Trace the requirement backward`, never a dash.

**Four-item lists by default.** Three only where a fourth does not exist. Two is fine. Seven is fine.

**No emoji in headers.** Anywhere, including footers.

**American English throughout.**

**Nothing unfinished ships.** No placeholder rows, no bracketed instructions left in a template, no section written to be filled in later.

---

## Commits

One artifact per commit where practical, straight to `main`. No pull requests, since this is a single-author repository.

```
Add Post 19 artifact: Unhappy Path Mapping Framework
Add branch reference: ISO 20022 CBPR+ Knowledge Pack
Update Post 19 artifact: corrected screening sequence
Update README: add Post 19 row
```

No prefixes, no trailing period, no emoji, no em dash.

---

## Adding a File

**Step 1: Decide which kind it is.** Post artifact or branch reference. Everything else follows from that.

**Step 2: Check it against the selection test.** The four criteria live in [CONTRIBUTING.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/CONTRIBUTING.md).

**Step 3: Write header, body, footer.** All three. Never two of the three.

**Step 4: Add the relations in both directions.** New file to old, and old file back to new, in the same commit.

**Step 5: Update the indexes.** A post artifact adds a row to the root README table and an entry in `artifacts/README.md`. A branch reference updates `artifacts/README.md` only where it changes a task route.

---

## Related Artifacts

* [CONTRIBUTING.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/CONTRIBUTING.md) - The editorial standard that sits on top of these mechanics
* [artifacts/README.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/README.md) - The conventions here applied across the published set

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
