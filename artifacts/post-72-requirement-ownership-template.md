<!-- LinkedIn: -->

# Requirement Ownership Template

**Series:** Systems Analyst Notes  
**Post:** 72  
**Phase:** 10 New Additions  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Puts one accountable owner and one informed list on every requirement, and says what happens when the owner changes. Add the block to the top of each requirement and stop approval while the owner, the informed list or the ownership date is empty.

---

## 1. The required pair

Three fields are required: the pair of `Owner` and `Informed`, plus `Owner since`, which the approval gate checks against the change log. `Thread` is supporting context.

| Field | Rule | Required |
|---|---|---|
| `Owner` | One named person with a role. A team, a channel or a distribution list is rejected | Yes |
| `Informed` | A list of people or roles who receive the change. It can be long, and it never replaces the owner | Yes |
| `Owner since` | Date the current owner accepted. It matches the latest owner row in the change log | Yes |
| `Thread` | What the owner answers for beyond the ticket: services, data and process the requirement depends on | Supporting |

The distinction between the first two is the point of the template. Informed people receive the change. The owner answers for it: when the rule moves, when a downstream service asks why, when an audit asks who decided.

---

## 2. The block to paste

```
Owner:        [name], [role]
Informed:     [role or name], [role or name], [role or name]
Owner since:  YYYY-MM-DD
Thread:       [services, data and process this requirement depends on]
```

---

## 3. Four rules

**Rule 1: One name.** Two owners is no owner, because each assumes the other answers. If the work is shared, one person is accountable. The others are recorded wherever the team tracks who does the work. This template only fixes who answers.

**Rule 2: Owner of the thread.** The owner answers for the platform, the data and the process the requirement depends on, not only for whether the ticket was written. When a requirement splits into smaller ones, the thread decides who owns each piece.

**Rule 3: Agents get an owner too.** Any agent that reads or acts on the requirement has one accountable owner, written beside the permission set it holds. A login with a customer's credentials does not identify the agent's owner. Verify ownership in the agent register and record a finding if it is missing.

**Rule 4: Changes need a successor.** An owner change is complete only when the new owner has acknowledged it in the change log, in the same change that updates `Owner since`.

---

## 4. Changing an owner

Four steps, done in one change.

**Step 1: Name the successor.** The current owner writes the successor's name into the change log row, not into a chat message.

**Step 2: Get the acknowledgment.** The successor confirms in the same row. An owner who has not acknowledged is not yet the owner.

**Step 3: Update the block.** `Owner` and `Owner since` change together.

**Step 4: Check the dependent records.** Open delivery items, decision records and agent registers that name the old owner get updated or flagged.

---

## 5. The agent row

Illustrative and genericized. Agents that touch a requirement get their own short record.

| Field | Value |
|---|---|
| `Agent` | Screening triage agent |
| `Owner` | Alex Morgan, Compliance operations lead (fictional) |
| `Permission set` | Read-only on the screening queue, no write access |
| `Last permission review` | 2026-08-18 |

---

## 6. A worked example

Illustrative and genericized, using the settlement retry requirement from the change log example.

```
Owner:        Jordan Lee, Settlement service lead (fictional)
Informed:     Compliance lead, Mexico corridor operations, QA
Owner since:  2026-08-18
Thread:       Settlement service config, retry limit ADR, integration spec section 4.2
```

The compliance lead appears under `Informed` and not under `Owner`, even though they requested the last change. They receive every change to this requirement. The settlement service lead answers for it.

---

## 7. Approval gate

Four checks before a requirement moves to Approved.

1. `Owner` holds exactly one name, and the name is a person.
2. `Informed` is filled in and does not repeat the owner.
3. `Owner since` matches the latest owner row in the change log.
4. Every agent that reads or acts on this requirement has an owner and a permission set on record.

A requirement that fails check 1 is the one that passes review with five thumbs-up and no one to ask six weeks later.

---

## Related Artifacts

* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - The five columns where an owner change and its acknowledgment get recorded
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Names the owner of every service before a requirement splits across them

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
