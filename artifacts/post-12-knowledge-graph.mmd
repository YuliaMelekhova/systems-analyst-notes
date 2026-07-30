<!--
Post: 12
Title: Knowledge Graph — Mapping How Information Actually Connects
Phase: 2 — The Knowledge Chapter
LinkedIn: [link once published]
-->

%%{init: {'theme': 'neutral', 'themeVariables': {'fontSize': '14px'}}}%%

graph TD

  %% ── Business Rules ──────────────────────────────────────────
  BR["🔷 Business Rule\nCross-Border Transfer Limit\n(US → LatAm)"]

  %% ── API Contracts ───────────────────────────────────────────
  API1["📄 API Contract\npain.001\n(Payment Initiation)"]
  API2["📄 API Contract\npacs.008\n(Credit Transfer)"]

  %% ── Compliance Constraints ──────────────────────────────────
  COMP_BR["⚠️ Compliance Constraint\nBrazil — BCB Resolution 521\nLGPD data residency"]
  COMP_MX["⚠️ Compliance Constraint\nMexico — CNBV Fintech Law\nAML reporting threshold"]
  COMP_US["⚠️ Compliance Constraint\nUS — BSA / FATF\nSanctions screening"]

  %% ── Architecture Decision Records ───────────────────────────
  ADR1["📋 ADR #012\nSettle Brazil corridor\nvia VASP channel"]
  ADR2["📋 ADR #017\nShared pacs.008 schema\nUS–MX and US–BR corridors"]

  %% ── Specification ───────────────────────────────────────────
  SRS["📑 SRS v2.1\nCross-Border Payment\nFlow Specification"]

  %% ── Source Requirement ──────────────────────────────────────
  REQ["🗂️ Requirement\nBR-0041\nInitiate cross-border transfer"]

  %% ── Relationships ───────────────────────────────────────────
  BR -->|"governs"| API1
  BR -->|"governs"| API2

  API1 -->|"constrained by"| COMP_BR
  API1 -->|"constrained by"| COMP_US
  API2 -->|"constrained by"| COMP_MX
  API2 -->|"constrained by"| COMP_US

  API1 -.->|"shared schema rail"| API2

  COMP_BR -->|"motivated"| ADR1
  COMP_MX -->|"motivated"| ADR2
  COMP_BR -->|"motivated"| ADR2

  ADR1 -->|"traces to"| REQ
  ADR2 -->|"traces to"| REQ
  SRS   -->|"specifies"| API2
  SRS   -->|"traces to"| REQ

  %% ── Styles ──────────────────────────────────────────────────
  classDef rule    fill:#1B2A4A,color:#fff,stroke:none
  classDef contract fill:#5B6B84,color:#fff,stroke:none
  classDef compliance fill:#C1502E,color:#fff,stroke:none
  classDef decision fill:#1B2A4A,color:#fff,stroke:#AFB9C8,stroke-width:1px
  classDef spec    fill:#5B6B84,color:#fff,stroke:none
  classDef req     fill:#AFB9C8,color:#1B2A4A,stroke:none

  class BR rule
  class API1,API2 contract
  class COMP_BR,COMP_MX,COMP_US compliance
  class ADR1,ADR2 decision
  class SRS spec
  class REQ req
