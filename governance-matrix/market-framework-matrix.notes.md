# Market Framework Matrix Notes

Series: Systems Analyst Notes
Branch: Governance Matrix
Author: Yulia Melekhova
Published: 2026

## Purpose

The header and footer for `market-framework-matrix.csv`, which cannot carry them itself, plus the reading rules the matrix depends on. Read this before treating any cell in the CSV as an answer.

---

## How to Read the Matrix

**The market columns answer applicability, not effort.** A cell reading `Applies` says the framework reaches the market. It says nothing about how much work compliance takes, which depends on the product and the data.

**`Extraterritorial` is the most expensive value in the matrix.** It means a framework belonging to another jurisdiction reaches an operation in this one. Teams scope by where the company is incorporated and get surprised by where the customers are. The EU AI Act row is the clearest case: a credit model built in Bogota for a customer base that includes EU residents is in scope for an Annex III use case.

**`Not applicable` means today.** Brazil's PL 2338 is the row to watch. It sits with the Chamber of Deputies and would move several cells if enacted.

**Binding by contract is still binding.** PCI DSS is not law in any of the four markets, and it will stop a payment product faster than most statutes, because the acquirer enforces it directly.

**The overlap column carries the real value.** Applicability is findable. The interaction between two frameworks that both apply, and the point where one uses a different word for the same control, is where the time goes.

---

## What the Matrix Deliberately Leaves Out

Sector-specific supervisory circulars. The CNBV in Mexico, the Banco Central do Brasil and the Superintendencia Financiera in Colombia each publish rules that bind harder and change faster than the frameworks listed. Those belong in a separate market-entry document, because they need a maintenance owner and a review date.

Employment and consumer protection law touching automated decisions. Real, and outside the scope of a governance matrix built for AI and data.

---

## Maintenance

Content verified as of August 2026. Three rows carry a known short shelf life and should be checked before any scoping decision rests on them:

1. PL 2338/2023, on any movement in the Chamber of Deputies.
2. The EU AI Act rows, since Digital Omnibus implementation continues.
3. The CCPA row, since the automated decision-making rules phase in on their own schedule.

The matrix is a starting position for a conversation with counsel. It is not the conversation, and it is not legal advice.

---

## Related Artifacts

* [stride-threat-modeling/payment-initiation-stride.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/stride-threat-modeling/payment-initiation-stride.md) - Which of the threat controls there are regulatory obligations depends on these rows
* [knowledge-packs/iso-20022-cbpr-plus.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/iso-20022-cbpr-plus.md) - The travel rule row and the structured address deadline are the same data quality problem
* [templates-quality-rules/readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) - Regulatory traceability is one of the readiness gates a requirement has to clear

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
