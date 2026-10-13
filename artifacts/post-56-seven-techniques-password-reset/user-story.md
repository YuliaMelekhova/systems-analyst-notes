# User Story: Password Reset by OTP

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Puts the reason for a requirement on one card and attaches acceptance criteria a tester can check. Reach for it when the reader needs to know why the feature exists before anything about how it works.

---

## Template

```
As a [role],
I want [capability],
so that [outcome].
```

Acceptance criteria follow the card, one per behavior, written as: Given [state], when [action], then [result]. Each criterion carries the ID of the business rule it depends on, so a changed rule points back to the criteria it touches.

---

## Worked example: REQ-AUTH-014

```
As a customer who has forgotten my password,
I want to reset it with a one-time code sent to my registered mobile number,
so that I can regain access without calling support.
```

**AC1:** Given a customer on the reset screen, when they submit a mobile number, then the screen shows the same confirmation whether or not the number belongs to an account (BR-08).

**AC2:** Given a registered number, when the request limits allow it, then a 6-digit code is sent by SMS to the number on the account (BR-01, BR-02, BR-05).

**AC3:** Given a code entered and a password submitted inside 5 minutes of the request, when the code is verified and the password is valid, then the new password replaces the old one (BR-03, BR-06).

**AC4:** Given 2 earlier incorrect entries, when the customer enters a third incorrect code, then the code is invalidated and the account is locked for 30 minutes (BR-04).

**AC5:** Given a verified code and a valid password, when the customer saves the password, then all active sessions end and a confirmation SMS is sent (BR-07).

---

## What this card leaves out

The story does not say what the customer reads after a wrong code, which fields are stored, or which combinations of conditions lead to which outcome. Those answers live in `wireframe.md`, `data-mapping.md` and `decision-table.csv`. The numbers behind every criterion live in `business-rules.md`.

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
