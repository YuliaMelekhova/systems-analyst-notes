# Cross-Border Payments Glossary

Series: Systems Analyst Notes
Branch: Knowledge Packs
Author: Yulia Melekhova
Published: 2026

## Purpose

Payment terms that carry a different meaning depending on the jurisdiction, the message standard or the person in the room. Reach for it when a requirement uses one of these words and the reviewers appear to agree.

---

## How to Use This

The entries below are not definitions in the dictionary sense. Each one names an ambiguity, states which readings exist, and gives the disambiguation to write into a specification.

A term that means one thing to the payments team, another to compliance, and a third to the correspondent bank does not announce itself. Everyone reads their own meaning and the review passes. The failure surfaces during integration testing, or later.

Marked `HIGH` are the entries that have produced rework in practice rather than just confusion in a meeting.

---

## Message Roles

### Debtor and Creditor `HIGH`

In ISO 20022, `Debtor` is the party whose account is debited, meaning the payer, and `Creditor` is the payee. In ordinary accounting usage, a debtor is someone who owes you money, which is close to the opposite. An analyst arriving from a finance background reads `Debtor` in a pacs.008 mapping table and maps it to the wrong entity.

**In a spec:** use `Debtor (payer)` and `Creditor (payee)` on first use in every document, and keep the parenthetical in field mapping tables. It looks redundant. It has prevented a mapping error more than once.

### Agent and Party

In ISO 20022 an `Agent` is a financial institution in the chain and a `Party` is a person or organization. The distinction drives which address rules apply: for agents, supplying a BIC remains a valid alternative to name and address under the CBPR+ structured address requirement, and for parties it does not.

Outside the standard, "agent" often means a retail location or a distribution partner in a remittance network, which is a different concept entirely and common in LatAm corridors.

**In a spec:** write `Agent (FI)` when using the ISO sense, and pick a different word for the retail sense.

### Intermediary Agent and Correspondent

Overlapping but not identical. `IntermediaryAgent1` and its siblings are specific ISO 20022 fields. Correspondent describes a commercial banking relationship, and a correspondent may occupy the intermediary agent field, the creditor agent field, or neither.

**In a spec:** name the field when the field is what matters, and name the relationship when the relationship is what matters. Do not use one word for both.

---

## Money Movement Lifecycle

### Clearing and Settlement `HIGH`

Clearing is the exchange of payment instructions and the calculation of what is owed. Settlement is the actual transfer of value that discharges the obligation. A payment can be cleared and unsettled, which is a real state that systems have to represent.

The gap matters most where the two happen at different times. In a batch ACH-style rail they can be hours or days apart. In an instant rail they are effectively simultaneous, which is exactly why teams that grew up on instant rails collapse the two concepts and then hit a corridor where they cannot.

**In a spec:** never let a status called `completed` cover both. If the system supports any rail with a clearing and settlement gap, the status model needs two states.

### Value Date, Settlement Date and Posting Date

Value date is when funds are treated as available for interest and finality purposes. Settlement date is when the transfer between institutions occurs. Posting date is when the entry appears on a statement. The three coincide often enough that teams assume one field is sufficient, and they diverge across time zones, cut-off times and weekends.

The CBPR+ structured address requirement makes this concrete: a payment initiated before November 14, 2026 with a value date on or after it needs a compliant address. A system storing only an initiation timestamp cannot answer whether a given payment is in scope.

**In a spec:** three fields, three definitions, and a stated rule for which one drives each business decision.

### Cut-Off Time

Ambiguous between the rail's cut-off, the correspondent's cut-off, and the internal cut-off the operations team applies to leave itself room. A payment submitted at 15:50 might be same-day by one definition and next-day by two others.

**In a spec:** every cut-off carries an owner and a time zone. `16:00` with neither is not a requirement.

### Straight-Through Processing

Means fully automated end to end in one organization, and "did not require manual repair at our institution" in another. STP rate figures from two institutions are frequently not comparable.

**In a spec:** define the measurement boundary before stating a target.

---

## The Reversal Family `HIGH`

This group produces more incorrect requirements than any other, because five distinct operations share overlapping everyday words.

| Operation | What it is | ISO 20022 shape |
|---|---|---|
| Cancellation | Stopping a payment before it is executed | camt.055 or camt.056 depending on the initiator |
| Recall | Asking a receiving institution to return funds already sent | camt.056, answered by camt.029 |
| Return | The receiving side sending funds back | pacs.004 |
| Refund | A commercial act between the two counterparties, a new payment in the opposite direction | A fresh pacs.008 |
| Chargeback | A card-network dispute process with its own rules and timelines | Outside ISO 20022 payment messages entirely |

A cancellation is a request that may be refused. A refund always succeeds mechanically because it is just another payment. A chargeback follows scheme rules and involves an arbiter. Requirements that say "the user can cancel the payment" without stating which of these is meant get implemented as whichever one the developer assumed.

**In a spec:** pick the word from the table, and state the point in the flow after which the operation changes identity.

---

## Regulatory Identity

### Beneficiary and Beneficial Owner `HIGH`

Beneficiary in a payment context is the payee, the party receiving the funds. Beneficial owner in an AML context is the natural person who ultimately owns or controls a legal entity. The words look related and refer to different things, and both appear in the same onboarding conversation.

Thresholds for beneficial ownership vary by market and by rule. Twenty-five percent is the common figure in US customer due diligence, and other markets and sectors apply different tests, including control tests with no percentage at all.

**In a spec:** `Beneficiary (payee)` and `Beneficial owner (UBO)`, always spelled out, and never abbreviated to a shared short form.

### KYC, CDD and EDD

KYC is the broad practice. CDD is the defined set of checks. EDD is the intensified version applied to higher-risk relationships. Teams use KYC as an umbrella for all three, then write a requirement saying "KYC is completed" that cannot be evaluated because it does not say which checks.

**In a spec:** name the check set, not the umbrella.

### Screening and Monitoring

Screening compares a party against lists at defined points, typically onboarding and transaction. Monitoring watches behavior over time for patterns. They use different data, run on different schedules and fail in different ways.

**In a spec:** a requirement mentioning "AML checks" without distinguishing these is not ready for build.

### Domestic and Cross-Border

A payment can be domestic by rail and cross-border by parties. A transfer between two accounts in the same country where one holder is non-resident sits differently for reporting than the rail suggests. The structured address requirement follows the same logic: it reaches domestic payments carrying a cross-border leg.

**In a spec:** define which attribute drives the classification for each rule, because different rules use different ones.

---

## Institutional Categories

The same product carries a different licence name in each market, and the obligations attached to each name are not equivalent. This is the fastest way for a market-entry plan to be wrong in a way that looks right.

| Market | Category for a non-bank holding customer funds | Supervisor |
|---|---|---|
| European Union | Electronic Money Institution (EMI) | National competent authority |
| United States | Money transmitter, licensed state by state | State regulators, with FinCEN registration |
| Mexico | Institución de Fondos de Pago Electrónico (IFPE) under the Ley Fintech | CNBV, with Banco de México for operational rules |
| Brazil | Instituição de Pagamento, by modality | Banco Central do Brasil |
| Colombia | Sociedad Especializada en Depósitos y Pagos Electrónicos (SEDPE) | Superintendencia Financiera de Colombia |

Wallet and e-money are product words, not regulatory ones. Neither appears as a licence category in any of the five rows.

**In a spec:** write the licence category for the market being specified. Writing "wallet" leaves the reader to guess which obligations attach.

---

## Local Rails Worth Naming Precisely

Instant, real-time and immediate get used interchangeably and mean different things per rail.

* **SPEI** (Mexico): near real-time interbank transfer operated by Banco de México, with defined operating windows.
* **Pix** (Brazil): instant payment scheme operated by Banco Central do Brasil, available continuously.
* **Transfiya** (Colombia): immediate interbank transfer between participating institutions, alongside ACH Colombia for batch flows.
* **FedNow and RTP** (United States): two separate instant rails with different participants, alongside ACH and Fedwire.

**In a spec:** name the rail. "Instant transfer" is not a rail, and the availability, limits and failure behavior differ enough that the distinction changes the requirement.

---

## Adding to This Glossary

One rule for whether a term belongs here: two people who both know the domain read it differently, and neither is wrong. Terms that are merely unfamiliar belong in a knowledge pack instead. Terms with one meaning that people occasionally forget belong in the project glossary.

---

## Related Artifacts

* [knowledge-packs/iso-20022-cbpr-plus.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/knowledge-packs/iso-20022-cbpr-plus.md) - The agent and party distinction decides which address rules apply
* [governance-matrix/market-framework-matrix.csv](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/governance-matrix/market-framework-matrix.csv) - Which supervisor enforces which category in each market
* [templates-quality-rules/requirement-antipatterns.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/requirement-antipatterns.md) - The reversible-looking irreversible action entry is the reversal family in requirement form

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
