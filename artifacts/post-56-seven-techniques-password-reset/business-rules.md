# Business Rules: Password Reset by OTP

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Holds every constraint and every number behind the reset in one place, each with an ID and an owner. Reach for it first when writing a requirement and again whenever a value changes, because the other six files in this folder cite these IDs.

---

## Template

Five columns per rule: ID, the rule in one sentence, the value, the owner who approves a change, and the files where the value appears. The last column turns a changed value into a checklist.

---

## Worked example: REQ-AUTH-014

| ID | Rule | Value | Owner | Appears in |
|---|---|---|---|---|
| BR-01 | The code is sent by SMS to the mobile number stored on the account, never to a number typed during the reset | Number on the account | Security | `user-story.md`, `use-case.md`, `decision-table.csv`, `data-mapping.md` |
| BR-02 | The code has 6 digits from a cryptographically secure generator and is stored only as a salted hash | 6 digits | Security | `user-story.md`, `use-case.md`, `decision-table.csv`, `data-mapping.md` |
| BR-03 | A reset attempt expires 5 minutes after it is created. Entering the code and submitting the password must both happen inside that window | 5 minutes | Security | All six other files |
| BR-04 | The third incorrect code entry invalidates the code and locks the account. While locked, the account cannot sign in and no code is issued for a new reset request. The screen still behaves as BR-08 requires, so a locked account looks the same as an unknown number | 3 entries, 30 minutes | Security | All six other files |
| BR-05 | At least 60 seconds pass between requests, and no more than 3 requests run per rolling hour, counted per mobile number. A new code replaces the previous one | 60 seconds, 3 per hour | Risk | All six other files |
| BR-06 | The new password can be set only on an attempt whose code has been verified, and it has at least 12 characters and differs from the current password | 12 characters | Security | All six other files |
| BR-07 | After a successful reset, all active sessions end and a confirmation SMS goes to the number on the account | All sessions | Product | `user-story.md`, `use-case.md`, `wireframe.md`, `decision-table.csv`, `data-mapping.md` |
| BR-08 | Screens and messages are identical whether or not the mobile number belongs to an account, including the lock message | Identical responses | Security | `user-story.md`, `use-case.md`, `wireframe.md`, `decision-table.csv`, `data-mapping.md` |

The owner approves a change to the value. Product owns the customer-facing outcome, Risk owns the limits that stop abuse of the SMS channel, and Security owns the rest.

---

## Changing a value

Step 1: Edit the rule and its value in this file, and get the owner's approval.

Step 2: Open each file in the `Appears in` column and update every place the old value is written.

Step 3: Add a row to the change log, using the five columns from the Post 24 template, naming every file touched.

Step 4: Re-read the completeness check in `decision-table.notes.md`, since a new limit can add or remove a row.

---

## What this list leaves out

It states constraints and says nothing about sequence, screens or storage. A rule such as BR-04 still needs a counter to live in, which `data-mapping.md` supplies, and a message to say it aloud, which `wireframe.md` supplies.

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
