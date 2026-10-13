# AI Regulatory Control Matrix

**Series:** Systems Analyst Notes  
**Branch:** Governance Matrix  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Maps eight architecture controls for an AI agent in a payment flow to relevant provisions and control objectives across seven regulatory and voluntary frameworks. Use it when one control needs supporting evidence for several regimes, or when a new market is added and the team needs to identify which existing controls already address its requirements.

---

## How to Read It

The file `ai-regulatory-control-matrix.csv` has one row per control and one column per law, standard, or guidance framework. Architecture controls run down the rows; regulatory and framework mappings run across the columns. A mapping can support compliance evidence without implying that a voluntary framework is legally binding.

Read across a row to see which frameworks a control supports. C01, the versioned system record, has six `Mapped` cells; SR 26-2 is marked `Excluded` for the generative or agentic AI scenario covered by this artifact.

Read down a column to compare what a source directly addresses and where a control has no direct match. In the Colombia column, C02 (fixed human approval checkpoint) is `Unmapped`, while C07 (customer review route) is `Mapped` to transparency and information rights, supplemented by the regulator's 2024 AI circular. The circular does not, by itself, create a direct fixed-approval-checkpoint provision for C02 in the matrix.

Every control row assumes a generative or agentic system. SR 26-2 explicitly excludes those models from its scope. Other model types must be assessed against the guidance separately; the `Excluded` label is not a general exemption from institutional risk governance.

**Visual summary:** The LinkedIn image shows six selected controls (C01, C02, C04–C07). The CSV contains all eight, including C03 (decision log) and C08 (personal-data masking).

---

## Cell Types

Every cell starts with one of three prefixes. A blank cell would hide the difference between no identified mapping and a formal exclusion, so none is left blank.

| Prefix | Meaning | What to do |
|---|---|---|
| `Mapped` | A cited provision or framework objective supports the control | Cite the source and record any applicability conditions |
| `Unmapped` | No direct provision or objective was identified in the sources reviewed | Keep the control where another framework or the risk assessment justifies it; document the gap |
| `Excluded` | The framework explicitly places the relevant system or activity outside its scope | Record the exclusion and identify any separate governance or risk-control requirements |

A possible fourth cell type, `Pending`, can be used when a framework applies to the system but agent-specific guidance has not yet been issued. It is not used in this CSV and is different from a column status of *adopted but not yet applicable*.

---

## Column Status

Each column has one of four lifecycle statuses: **in force**, **adopted but not yet applicable**, **proposed**, or **withdrawn**. Add qualifiers for phased applicability and for voluntary standards or guidance. Record the relevant dates and recheck the status when using the mapping; a published voluntary framework is not automatically a legal obligation.

| Column | Status | Reference |
|---|---|---|
| EU AI Act | In force (phased applicability) | Article 50 transparency applies since August 2, 2026. Annex III high-risk obligations apply from December 2, 2027 and Annex I from August 2, 2028, under Regulation (EU) 2026/1744, in force July 27, 2026 |
| NIST AI RMF | In force (voluntary framework) | AI RMF 1.0, January 2023 |
| ISO/IEC 42001 | In force (voluntary, certifiable standard) | Published December 2023 |
| US SR 26-2 | In force | April 17, 2026, with OCC Bulletin 2026-13 and FDIC FIL-15-2026. Replaced SR 11-7. Generative and agentic AI are outside scope and an AI-specific consultation is anticipated |
| Brazil LGPD | In force | Law 13.709 of 2018, applying since September 2020 |
| Mexico LFPDPPP | In force | New law effective March 21, 2025, replacing the 2010 law. Supervision moved from INAI to the Secretariat of Anti-Corruption and Good Governance |
| Colombia Law 1581 | In force | Law 1581 of 2012. SIC External Circular 002 of August 21, 2024 applies to personal data in AI systems |

---

## Scope and Verification

Cells were drafted from the framework texts and from law-firm summaries of the 2025 and 2026 changes. ISO/IEC 42001 Annex A numbers and NIST AI RMF 1.0 subcategory numbers were checked against published crosswalks and official-text mirrors. Check EU AI Act, LGPD and Law 1581 article numbers against the primary texts before quoting a cell in a compliance file.

Mexico's cells cite topics rather than articles, because the 2025 article numbering has not been checked against the Official Gazette text.

Under the EU AI Act, Articles 9 to 15 and 26 apply to high-risk systems. A system that only detects fraud sits outside that tier under Recital 58, while creditworthiness assessment and biometric identification stay inside it. State which function the system performs before reading the EU column.

---

## Adding a Column

Step 1: Set the column status: in force, adopted but not yet applicable, proposed, or withdrawn. Add dates and note when a framework is voluntary or has phased applicability.

Step 2: Fill every row. Each of the eight controls gets `Mapped` with a provision or objective, `Unmapped` with a documented lack of direct match, or `Excluded` with an explicit scope basis.

Step 3: Distinguish scope from applicability dates. Use `Excluded` only for an explicit scope exclusion. If future guidance is expected but the system is already in scope, consider a separate `Pending` cell type; do not confuse it with an adopted-but-not-yet-applicable column.

Step 4: Add a ninth control only when a column asks for something no row answers. A control that no column cites is a candidate for removal.

---

## Related Artifacts

* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Walks through two regimes that conflict on one transaction, the case a cross-column matrix has to carry
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Names the owner of each service before a control is mapped to the obligations it answers
* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - Records the decision that resolves a cross-column conflict, so the reasoning outlives the ticket
* [artifacts/post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) - Handles the client tier where a change is mandated externally, which is what a dated column describes

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
