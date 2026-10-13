# Decision Table: Password Reset by OTP

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Notes for `decision-table.csv`, which lists every combination of conditions in the reset flow with exactly one outcome each. Reach for the table when a developer needs logic with no gaps and no overlaps, and for these notes when reading it.

---

## How to read the table

Each row is one rule. Read the condition columns left to right, find the row that matches, and the action columns on the right say what happens. `Y` and `N` are yes and no. A dash means the condition does not matter for that rule.

The rules sit in three stages, evaluated in the order the customer meets them: `request` (D01 to D04), `verify` (D05 to D09) and `submit` (D10 to D13). Inside a stage, the rules never overlap, so at most one row matches.

---

## Conditions

| Column | True (Y) when |
|---|---|
| `prior_requests_lt_3` | Fewer than 3 reset requests came from this mobile number in the past hour (BR-05) |
| `wait_60s_met` | At least 60 seconds have passed since the last request from this number (BR-05) |
| `account_usable` | The number matches an account and the account is not locked (BR-04, BR-08). When N, the attempt is still created so the screen matches BR-08, but no code is issued |
| `within_5_min` | The attempt was created less than 5 minutes ago (BR-03) |
| `code_matches` | The entered code matches the stored hash (BR-02) |
| `failed_before_entry` | Count of incorrect entries before this one: 0, 1 or 2 (BR-04) |
| `attempt_verified` | The attempt status is VERIFIED, meaning the code was checked and accepted (BR-06) |
| `password_meets_rule` | The new password has at least 12 characters and differs from the current one (BR-06) |

---

## Completeness check

The request stage has 3 yes-or-no conditions, so 8 combinations exist. D01 covers 4 of them (any wait, any account state, limit reached), D02 covers 2, and D03 and D04 cover 1 each.

The verify stage splits first on expiry. D05 covers every expired case, and with the window still open, one row covers a matching code (D06) and three rows cover a wrong code at 0, 1 or 2 earlier failures (D07 to D09). A fourth wrong code never appears as a row because D09 invalidates the code on the third.

The submit stage has four outcomes: expired (D10), code never verified (D11), rejected password (D12) and completed reset (D13). D11 closes a gap the first version had: without `attempt_verified`, a request that skipped the code check could reach the password step.

---

## What this table leaves out

It decides outcomes and stores nothing. Where each outcome writes its state is in `data-mapping.md`, and the text behind each `message_id` is in `wireframe.md`.

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
