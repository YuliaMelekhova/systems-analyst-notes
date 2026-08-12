# What Gets Into This Repo

**Series:** Systems Analyst Notes  
**Scope:** Repository  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

The selection criteria applied before anything is committed here, written down so the standard is visible rather than implied. This is a single-author reference repository, so the document describes how the author decides, not how to submit a pull request.

---

## The Test

An artifact ships when it passes all four.

**1. It was built for a real problem, not for the repository.** Every file here started as something needed on a piece of work, then generalized. A template written to fill a gap in the repository structure reads differently from one that has been used, and the difference shows in the parts that are specific.

**2. It is specific enough to be wrong.** A document nobody could disagree with is a document nobody needed. The address knowledge pack commits to a position on hybrid versus fully structured. The antipattern file names failures that some teams will argue are fine. That is the intended state.

**3. It cannot be found in five minutes elsewhere.** Reformatting freely available material adds a copy, not a contribution. The question before writing is what this file has that the first page of search results does not, and if the answer is formatting, the file does not get written.

**4. Someone could use it tomorrow.** Not read it and agree. Use it. Every artifact ends with something to apply: a field set, a gate, a question list, a decision rule.

---

## What Does Not Ship

**Generic BA material.** Stakeholder matrices, SWOT, the Epic and Feature and Story hierarchy, interview question lists. Well covered elsewhere, and covered better by people who specialize in it.

**Tool tutorials.** How to configure a specific product is documentation the vendor owns and updates. It goes stale here within a release cycle.

**Templates with no worked content.** A section-heading skeleton with `[describe the problem here]` inside it transfers no knowledge. If the example cannot be written, the template is not understood well enough to publish.

**Anything traceable to a specific employer.** Every scenario here is genericized. Cross-border payment flows, LatAm corridors and card issuance appear as realistic constructions, not as a description of any company's system.

**Third-party visual material.** Diagrams are authored and committed as source. Images from articles and vendor decks are read for angles and never reproduced.

---

## Two Kinds of File

**Post artifacts** live in `artifacts/`, named `post-NN-slug.ext`, and exist because a numbered post in the series called for a companion. They carry a post number and a phase, and one row in the root README table.

**Branch references** live in the five framework folders and stand on their own. They carry a branch name instead of a post number. They are added when the branch needs a working example of what belongs in it, or when a topic outgrows the post that raised it.

A branch reference can be linked from several posts. That is the point of the separation: the file is not owned by any one post and does not have to wait for one.

---

## Editing Published Files

Published post artifacts are corrected, not rewritten. A factual error gets fixed with a commit message naming what changed. Structure and argument stay as published, because the artifact is tied to a post that readers already have.

Branch references have no such constraint and are expected to change as standards move. The governance matrix and the address pack both carry verification dates for that reason.

---

## Format Rules

Naming, header and footer blocks, phase names, link format and file extension by content type live in [repo-guide.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/repo-guide.md). That file is the mechanical standard. This one is the editorial standard, and a file has to pass both.

---

## Reuse

Everything here is written to be taken and adapted. Attribution is welcome and not demanded. If something gets used and turns out to be wrong or incomplete in practice, that is worth hearing about through the LinkedIn link below, and corrections get made.

---

## Related Artifacts

* [repo-guide.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/repo-guide.md) - The mechanical conventions this document sits on top of
* [artifacts/README.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/README.md) - What has passed the test so far, grouped by what the file does

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
