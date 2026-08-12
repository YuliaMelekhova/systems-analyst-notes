<!--
Post: 12
Title: Knowledge Graph — Mapping How Information Actually Connects
Phase: 2 — The Knowledge Chapter
LinkedIn: [(https://www.linkedin.com/posts/yuliamelekhova_systemsanalysis-knowledgemanagement-fintech-activity-7488722623741231104-nh_6?utm_source=social_share_send&utm_medium=member_desktop_web&rcm=ACoAABW2QzcBN4fI21bG0ls7u2nHq-ooXTFxjEU)]
-->

# Knowledge Graph — Payment Domain

A knowledge graph for a cross-border payment platform covering US, Brazil, and Mexico corridors.
Nodes represent distinct knowledge artifacts. Edges represent dependency and traceability relationships.

```mermaid
%%{init: {'theme': 'neutral', 'themeVariables': {'fontSize': '14px'}}}%%

graph TD

  %% ── Business Rules ──────────────────────────────────────────
  BR["Business Rule
  Cross-Border Transfer Limit
  (US → LatAm)"]

  %% ── API Contracts ───────────────────────────────────────────
  API1["API Contract
  pain.001
  (Payment Initiation)"]
  API2["API Contract
  pacs.008
  (Credit Transfer)"]

  %% ── Compliance Constraints ──────────────────────────────────
  COMP_BR["Compliance Constraint
  Brazil — BCB Resolution 521
  LGPD data residency"]
  COMP_MX["Compliance Constraint
  Mexico — CNBV Fintech Law
  AML reporting threshold"]
  COMP_US["Compliance Constraint
  US — BSA / FATF
  Sanctions screening"]

  %% ── Architecture Decision Records ───────────────────────────
  ADR1["ADR #012
  Settle Brazil corridor
  via VASP channel"]
  ADR2["ADR #017
  Shared pacs.008 schema
  US–MX and US–BR corridors"]

  %% ── Specification ───────────────────────────────────────────
  SRS["SRS v2.1
  Cross-Border Payment
  Flow Specification"]

  %% ── Source Requirement ──────────────────────────────────────
  REQ["Requirement
  BR-0041
  Initiate cross-border transfer"]

  %% ── Relationships ───────────────────────────────────────────
  BR -->|governs| API1
  BR -->|governs| API2

  API1 -->|constrained by| COMP_BR
  API1 -->|constrained by| COMP_US
  API2 -->|constrained by| COMP_MX
  API2 -->|constrained by| COMP_US

  API1 -.->|shared schema rail| API2

  COMP_BR -->|motivated| ADR1
  COMP_MX -->|motivated| ADR2
  COMP_BR -->|motivated| ADR2

  ADR1 -->|traces to| REQ
  ADR2 -->|traces to| REQ
  SRS   -->|specifies| API2
  SRS   -->|traces to| REQ
```

---

## How to read this graph

- **Solid arrows** — direct dependency or governance relationship
- **Dashed arrow** — shared schema rail between two corridors (US–BR and US–MX both use pacs.008)
- **Compliance nodes** propagate the widest: a regulatory update in Brazil touches ADR #012, ADR #017, and both API contracts

## How to adapt this to your domain

1. Replace business rules with your own (lending limits, FX conversion rules, fee structures)
2. Replace compliance constraints with the regulations relevant to your markets
3. Keep the same relationship types: governs, constrained by, motivated, traces to, specifies
4. Add nodes for data models or event schemas if your system is event-driven

The value is not in the specific nodes — it's in making the dependency chain visible before a change propagates through the system.
