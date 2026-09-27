<!-- LinkedIn: -->

# Multi-Agent Documentation Pipeline Map

**Series:** Systems Analyst Notes
**Post:** 47
**Phase:** 6 AI Agents at Work
**Author:** Yulia Melekhova
**Published:** 2026

## Purpose

Maps the coordinator-to-specialist shape of a documentation pipeline, names all five infrastructure layers that must be specified before any agent is built, and states the cache layer technique that actually preserves decisions across a BRD-to-SRS-to-ADR handoff chain.

---

## 1. Pipeline shape

```
                        COORDINATOR
                   (decomposes + routes)
                           |
         POLICY LAYER (what each step may read, call, sign off)
                           |
         +------------------+-----------------+
         |                  |                 |
    RESEARCH STEP      DRAFTING STEP    VALIDATION STEP
    Gather source      Produce the      Check draft vs.
    material           artifact         source before
                                        human sees it
                                              |
                                       HUMAN REVIEW
```

The coordinator routes. The policy layer governs. The three steps each have one job. Human review sits at the end of the validation step, not after every step.

None of this requires a standalone tool. The same shape runs inside Jira, Confluence, and Slack via API integrations. The coordinator ingests an issue, routes it to the appropriate steps, auto-updates fields, and posts a summary as a comment. The agent is woven into tools the team already uses.

---

## 2. Three event routes

Most documentation pipelines handle three event types. Each routes differently.

**Route 1: New documentation request**
Trigger: New item in Jira or Notion with status "Needs documentation"
Path: Coordinator ingests → classifies by request type → routes to Research + Drafting + Validation → posts draft for human review → updates status on approval

**Route 2: Source update**
Trigger: A referenced ADR, requirement, or spec changes in the knowledge base
Path: Coordinator identifies downstream artifacts affected → routes to Validation step → flags impacted documents for re-review → notifies owner

**Route 3: Human rejection**
Trigger: Human reviewer returns an artifact as "Needs revision"
Path: Coordinator receives rejection signal + reason → routes to appropriate step (Drafting or Research, depending on reason) → re-runs from that step only → returns to Validation

---

## 3. The policy layer

The policy layer sits between the coordinator and each specialist step. It answers three questions per step:

- **What may this step read?** Named sources only. Not "everything in the knowledge base."
- **Which tools may this step call?** An allowlist, not the full tool registry.
- **Does this step's output require human sign-off before the next step receives it?** Named condition, not the coordinator's judgment.

Written as rules rather than as instructions embedded in each step's prompt, the same policy layer applies whether the coordinator is routing to a research step or a validation step. This is what makes the pipeline auditable: the rules are in one place and they do not change depending on which step is currently running.

---

## 4. Five infrastructure layers

Most teams build the agent steps first and discover these layers in production. The analyst specifies them before a single agent is built.

**Layer 1: Ingestion**
Fetches source material, chunks by one complete idea (not a fixed token count), enriches each chunk with metadata (effective date, jurisdiction, document status, version), and validates vectors before anything reaches an agent. Chunking sets the ceiling on retrieval quality. A chunk boundary that splits a compliance rule from its exception produces a retrieval that looks relevant and answers wrong.

**Layer 2: Cache**
Session state and working context so agents do not re-fetch the same source on every step. See Section 5 for the technique that matches this pipeline's failure mode.

**Layer 3: Hybrid Retrieval**
Keyword search plus vector search plus re-ranking. Retrieval quality should not depend on any single method. Metadata filtering is what keeps a similar-but-superseded document out of the answer. A current policy and a superseded one that reads almost identically look the same to similarity search; the effective date field is what tells them apart.

**Layer 4: Agentic Layer**
The coordinator handles conflict resolution and synthesis, not just routing. When two retrieval results disagree, the coordinator resolves the conflict before passing context downstream. If it cannot resolve it, it escalates to human review.

**Layer 5: Observability**
Tracks inter-agent latency, decision logic at each step, and the full multi-agent state simultaneously. This layer is what makes a post-incident review possible. Without it, the review sees what the final output was - not which step produced the error, why, and how it propagated.

---

## 5. Cache layer: which technique carries state

A sliding window keeps only the most recent turns and drops anything older. It fails the moment a decision from an early step needs to survive three handoffs later - which is the normal shape of a BRD-to-SRS-to-ADR chain.

Summarization compresses older state into a shorter description. The distortion compounds with every additional pass. A summarization step that runs once between two agents is a reasonable tradeoff. A summary of a summary of a summary, several handoffs deep, is where a decision quietly gets simplified into something nobody actually agreed to.

Structured entity extraction carries a small set of named fields between agents - confirmed decisions, current status, open questions - each one written once and updated rather than re-summarized. This is the technique that matches this pipeline's failure mode. The coordinator carries decisions, not narratives.

**Rule for the pipeline map:** Name which cache technique carries state across which handoff. Any handoff using narrative summarization needs a note saying so, because that is the specific point where compounding-loss failure becomes likely rather than theoretical.

---

## 6. Version transition: the staleness trap

When a regulatory deadline moves or a specification is updated, two versions of the affected artifact can remain retrievable at once. The agent has no way to prefer the current one over the superseded one unless the pipeline enforces it.

The fix: an explicit `active_version` flag set at the moment the new version is verified, not the moment the new chunks are inserted. There must never be a window where two contradictory versions are both marked eligible for retrieval.

The version-transition step needs a named owner, not just a schedule.

---

## 7. Self-check before shipping the pipeline spec

1. Are all five infrastructure layers named, with the chunking rule, filtering rule, and cache technique specified?
2. Is the policy layer written as rules, not as instructions embedded in each step's prompt?
3. Does the observability layer capture inter-agent latency and decision logic, not just final outputs?
4. Is the annotation flywheel specified? (Where do rejected outputs go, and how do they improve the next run?)
5. Does each event route have a named trigger, path, and terminal state?
6. Is the version-transition step for the ingestion layer covered, with a named owner?

---

## Related Artifacts

- [artifacts/post-46-agent-acceptance-criteria.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-46-agent-acceptance-criteria.md) - The thresholds this pipeline's outputs are measured against before any step is marked done
- [artifacts/post-48-loop-engineering-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-48-loop-engineering-spec.md) - Stop conditions and risk tiers for each step in this pipeline; the annotation flywheel definition
- [artifacts/post-41-ai-agent-instruction-standard.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-41-ai-agent-instruction-standard.md) - The instruction standard each specialist step in this pipeline is built against
- [artifacts/post-43-observability-requirements.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-43-observability-requirements.md) - The four log types the observability layer in this pipeline must capture

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
