<!-- LinkedIn: -->

# Decision Table Template

**Series:** Systems Analyst Notes  
**Post:** 58  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Gives a rule table in which every rule has a condition, an evidence source and an outcome, with needs review as a third result next to eligible and ineligible. Reach for it when an assistant answers questions that a written policy can settle, so that application code applies the rule and the model only explains the result.

---

## 1. Scope

A rule belongs in the table when four things are true.

| Test | Passes when |
|---|---|
| Facts | Every fact the condition needs can be read from a named system |
| Wording | The condition contains no judgment word such as "reasonable", "material" or "promptly" |
| Repeatability | The same facts always produce the same outcome |
| Ownership | One person or team approves the value and answers for a change to it |

A rule that fails any of the four goes to a person. So do exceptions, and so does policy language that two readers would interpret differently. The table leaves judgment with people and keeps guesses out of the software.

---

## 2. Who does what

| Actor | Does | Does not |
|---|---|---|
| Application code | Compares verified facts to the conditions, returns one outcome, records which rule fired | Ask the model what the outcome should be |
| Model | Explains the outcome in plain words, using only the outcome and the rule text | Decide an outcome, supply a missing fact, or add a claim the outcome does not support |
| Person | Handles needs_review rows and exceptions, records a rationale for each | Close a case without the evidence the rule listed |

The model never sees a rule table and then decides which row applies. Code picks the row. The model words the result.

---

## 3. The rule table

One row per rule. Six columns.

| Column | What goes in it | Rule |
|---|---|---|
| Rule ID | A stable identifier such as R-01 | Never reused, never renumbered. Same convention as the Post 56 business rules list |
| Condition | One testable statement | Thresholds are written as values with a unit, for example 14 days |
| Facts needed | The field names the condition reads | One line per fact, written the way the system names it |
| Evidence source | The system that holds each fact | Exactly one source per fact |
| Outcome | One value from the list in section 4 | A blank is a defect |
| Owner | The person or team that approves the value in the condition | A role is acceptable, a shared inbox is not |

---

## 4. Outcome values

Two groups, kept apart on purpose. Eligibility rules use the first three values. Completion rules use the last two.

| Value | Meaning | When it fires |
|---|---|---|
| `eligible` | The facts meet the condition | All facts present and the condition holds |
| `ineligible` | The facts fail the condition | All facts present and the condition does not hold |
| `needs_review` | The facts cannot settle the question | Any needed fact is missing, unreadable or contradictory |
| `completed` | The downstream system confirmed the action | The system of record reports success |
| `lookup_failed` | The system that holds the fact did not answer | Timeout, error or an unusable response |

The outcome field accepts only these values. Payments teams already work this way: sanctions screening returns clear, hit or no answer, and no answer holds the payment.

---

## 5. Eligibility and completion are separate rows

A customer can qualify for a refund while the refund has not been issued. These are two facts with two evidence sources, so they get two rows.

The application may say a customer qualifies once an eligibility row has fired. It may say the action happened only after a completion row has fired. Wording that merges the two ("your refund is on its way") needs both rows to have fired.

---

## 6. Needs-review rows

Every rule gets a needs_review row. A row is ready to ship only when all three fields below are filled.

| Field | What it holds | Example |
|---|---|---|
| Missing fact | The fact whose absence triggers the row | `purchase_date` |
| Review owner | The named role that picks the case up | Support team lead |
| Customer sees meanwhile | The exact message shown while the case waits | A holding message and a reply time |

The third field is the one that gets skipped. Without it, the screen shows whatever the model produces, which is the guess the row exists to prevent.

---

## 7. Tool failures

The lookup that fetches a fact can fail in four ways, and each one maps to a recorded state. Assuming the lookup succeeded brings the guess back at a different point.

| What the lookup did | State recorded | What the rule does |
|---|---|---|
| Returned the fact | The fact is used | The condition is evaluated |
| Succeeded but found no record | The fact is missing | The needs_review row fires |
| Timed out or returned an error | `lookup_failed` | Retry within the retry budget, then the needs_review row fires |
| Returned a value the schema rejects | The fact is unreadable | The needs_review row fires |

---

## 8. Worked example

A refund policy with a 14-day window. This is a constructed illustration, not a reported incident. Copy the table and replace the values with your own.

| Rule ID | Condition | Facts needed | Evidence source | Outcome | Owner |
|---|---|---|---|---|---|
| R-01 | Purchase is 14 days or fewer before today | `purchase_date`, `today` | `order_record` | `eligible` | Customer support operations |
| R-02 | Purchase is more than 14 days before today | `purchase_date`, `today` | `order_record` | `ineligible` | Customer support operations |
| R-03 | Purchase date is missing or unreadable | `purchase_date` | `order_record` | `needs_review` | Customer support operations |
| R-04 | Payment system reports the refund succeeded | `refund_status` | `payment_system` | `completed` | Payments operations |
| R-05 | Payment lookup times out or returns an error | `refund_status` | `payment_system` | `lookup_failed` | Payments operations |

Four cases run through it.

| Case | Facts | Rules that fire | What the model may say |
|---|---|---|---|
| A | Purchase 10 days ago, no refund yet | R-01 | The purchase qualifies for a refund |
| B | Purchase 15 days ago | R-02 | The purchase is past the 14-day window |
| C | Purchase date missing | R-03 | A team member is checking the order and will reply by email |
| D | Purchase 10 days ago, payment lookup times out | R-01 and R-05 | The purchase qualifies, and the refund status cannot be confirmed right now |

Case A is where an unsupported sentence usually appears. A draft that adds "and the money arrives within five days" has made a claim that no row supports. Section 9 removes it.

---

## 9. Claim check

Run on every draft answer before it reaches the customer.

**Step 1: Split the draft into single claims.** One fact per claim. "You qualify, and the money arrives within five days" is two claims.

**Step 2: Attach evidence to each claim.** The evidence is a fired rule ID or a fact returned by a named system. Nothing else counts.

**Step 3: Remove every claim without evidence.** Remove it entirely. Softening it ("usually within five days") keeps the claim and adds doubt, which is worse.

**Step 4: Log what was removed.** A removed claim is a signal about the prompt or the policy page, and it feeds the evaluation set.

| Draft claim | Evidence | Kept |
|---|---|---|
| The purchase qualifies for a refund | R-01 fired | Yes |
| The money arrives within five days | None | No |

---

## 10. Changing an existing outcome field

If a published API already returns a two-value eligibility field, adding `needs_review` is the new-enum-value case in section 4 of the Post 28 versioning policy. It is non-breaking only for clients that were told to tolerate unknown values. Decide that sentence before the third state ships, not after.

---

## 11. Review gate

Five checks before a rule table goes to build.

1. Does every rule have an ID, a condition without a judgment word, and a named owner?
2. Does every fact in a condition have exactly one evidence source?
3. Does every rule have a needs_review row with all three fields from section 6 filled?
4. Are eligibility and completion separate rows with separate evidence sources?
5. Does every tool state in section 7 map to a recorded state, with none mapped to an assumed success?

---

## 12. Known limits

The table settles rules with clear answers. Vague policy language still needs a person, and the table does not change that.

The claim check reduces errors without removing them. The checker can be wrong too, so keep as much of it as possible in plain code that matches claims against the outcome and the fired rule IDs.

The case for putting abstention in the software comes from Kalai, Nachum, Vempala and Zhang, "Why Language Models Hallucinate" (arXiv 2509.04664). Their argument is that most evaluations score a wrong answer and "I don't know" the same, which rewards guessing. It is the authors' thesis, and published critics dispute parts of it. The design holds either way.

The claim check follows Dhuliawala and colleagues, "Chain-of-Verification Reduces Hallucination in Large Language Models" (arXiv 2309.11495). The lookup requirement follows Yao and colleagues, "ReAct: Synergizing Reasoning and Acting in Language Models" (arXiv 2210.03629), whose tests used a public Wikipedia API rather than customer data. Test your own lookups before relying on that result.

---

## Related Artifacts

* [artifacts/post-39-hitl-checkpoint-spec.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-39-hitl-checkpoint-spec.md) - Shows where a needs_review case sits among the five checkpoint tiers and who approves it
* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - The payee verification result there is a multi-value outcome field defined as a contract, which is where a third state gets declared
* [artifacts/post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) - Section 4 decides whether adding a new outcome value breaks existing clients
* [artifacts/post-25-sequence-diagram.mmd](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.mmd) - The screening branch that gets no answer is this three-outcome pattern drawn as a conversation
* [artifacts/post-62-er-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-62-er-diagram.md) - Where each fact a rule needs is stored, and who writes it

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
