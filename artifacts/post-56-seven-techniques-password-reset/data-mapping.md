# Data Mapping: Password Reset by OTP

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Shows where each field comes from, where it lands and how it is transformed on the way. Reach for it when developers and data owners need to agree on what is stored, what is only compared and what must never be written down.

---

## Template

Five columns per row after the ID: source, target, type, transformation and the business rule that sets the behavior. A row with no rule ID has no owner, so it does not ship.

---

## Worked example: REQ-AUTH-014

Five tables are involved: `reset_attempt` (new for this requirement), `user`, `sms_outbox`, `session` and `auth_log`.

| ID | Source | Target | Type | Transformation | Rule |
|---|---|---|---|---|---|
| DM-01 | S1 `mobile_number` | `reset_attempt.mobile_number_e164` | string | Strip spaces and dashes, then normalize to E.164 | BR-05 |
| DM-02 | `user.mobile_number` | `reset_attempt.account_id` | uuid, nullable | Look up by the normalized number. Null when no account matches | BR-08 |
| DM-03 | System clock | `reset_attempt.expires_at` | timestamp, UTC | `created_at` plus 5 minutes | BR-03 |
| DM-04 | OTP Service output | `reset_attempt.otp_hash` | string, nullable | Salted hash of the 6-digit code. Null when no SMS was sent. The plain code is never stored | BR-02 |
| DM-05 | `user.mobile_number` | `sms_outbox.to_number` | string | Copied from the account, never from S1 | BR-01 |
| DM-06 | S2 `otp_code` | Compared with `reset_attempt.otp_hash` | not stored | Hash the entry and compare. The entry is discarded | BR-02 |
| DM-07 | Failed comparison | `reset_attempt.failed_count` | integer | Starts at 0. Add 1 per incorrect entry, up to 3 | BR-04 |
| DM-08 | Third failed comparison | `user.locked_until` | timestamp, UTC, nullable | Now plus 30 minutes. Written only when `account_id` is not null | BR-04 |
| DM-09 | Attempt outcome | `reset_attempt.status` | enum | OPEN, VERIFIED, EXPIRED, EXHAUSTED, SUPERSEDED, COMPLETED | BR-03, BR-04 |
| DM-10 | S3 `new_password` | `user.password_hash` | string | Written only when the attempt status is VERIFIED. Hashed with the platform's standard algorithm. Plain text is never stored | BR-06 |
| DM-11 | Reset completed | `session.revoked_at` | timestamp, UTC | Now, for every session where `session.user_id` equals `account_id` | BR-07 |
| DM-12 | Each step | `auth_log.event_type` | enum | RESET_REQUESTED, CODE_SENT, CODE_SEND_FAILED, CODE_FAILED, CODE_VERIFIED, ACCOUNT_LOCKED, PASSWORD_CHANGED | BR-04 |
| DM-13 | Attempt status at the event | `auth_log.otp_status` | enum | Copy of `reset_attempt.status`. The code itself is never logged | BR-02 |

`confirm_password` from S3 is compared with `new_password` and then discarded, so it has no row.

---

## What this mapping leaves out

It lists fields and says nothing about order or timing. The sequence of writes is in `use-case.md` and `bpmn.md`. The one thing it adds that no other file carries: `failed_count` needs a column, a starting value and a reset rule, and `account_id` and `otp_hash` both need to allow null, because BR-08 makes the flow run for numbers that match no account.

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
