# Use Case: Reset Password by OTP

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Walks one requirement as a main flow, alternate flows and exception flows, one numbered step at a time. Reach for it when testers need every path written down before the first test case is drafted.

---

## Template

Nine fields, in this order: ID and name, primary actor, supporting actors, preconditions, trigger, main flow, alternate flows, exception flows, postconditions. Alternate and exception flows each name the main-flow step they branch from, so a reader can trace every path back to the line that spawned it.

---

## Worked example: UC-AUTH-014

**Name:** Reset Password by OTP  
**Primary actor:** Customer  
**Supporting actors:** Auth Service, OTP Service, SMS Gateway  
**Preconditions:** The customer has a registered mobile number and cannot sign in.  
**Trigger:** The customer selects Forgot password on the sign-in screen.

### Main flow

1. The customer opens the reset screen (S1) and enters a mobile number.
2. The Auth Service checks the request limits (BR-05).
3. The Auth Service creates a reset attempt that expires in 5 minutes (BR-03) and looks up the account.
4. If the account is usable, the OTP Service generates a 6-digit code, stores its hash and hands the code to the SMS Gateway, which delivers it to the number on the account (BR-01, BR-02).
5. The Auth Service shows the code entry screen (S2) with message M-01 (BR-08).
6. The customer enters the code.
7. The Auth Service checks that the attempt has not expired, and the OTP Service compares the code with the stored hash.
8. The Auth Service opens the new password screen (S3).
9. The customer enters a new password twice.
10. The Auth Service checks that the attempt is still inside its 5 minutes, that its code was verified, and that the password meets BR-06.
11. The Auth Service replaces the password, ends all sessions and asks the SMS Gateway to send the confirmation (BR-07).
12. The Auth Service shows the done screen (S4).

### Alternate flows

**A1: Resend (from step 6).** The customer taps Resend after 60 seconds. The flow returns to step 2, and the new code replaces the previous one (BR-05).

**A2: Abandon (any step).** The customer leaves. The attempt expires after 5 minutes and the account is unchanged (BR-03).

**A3: Number format (step 1).** The customer types the number with spaces or dashes. The system normalizes it before the lookup in step 3.

### Exception flows

**E1: Limits exceeded (step 2).** The last request was under 60 seconds ago, or 3 requests already ran in the past hour. The customer sees M-06 or M-05, and no attempt is created (BR-05).

**E2: Number unknown or account locked (step 4).** No SMS is sent. The flow continues with M-01. Any code entered gets M-02, and the third one gets M-04 with nothing locked if no account exists (BR-04, BR-08).

**E3: Gateway rejects the SMS (step 4).** The failure is logged as CODE_SEND_FAILED. The customer still sees M-01 and can resend after 60 seconds (BR-08).

**E4: Attempt expired (step 7 or 10).** The customer sees M-03 and restarts through A1 (BR-03).

**E5: Wrong code, first or second time (step 7).** The customer sees M-02, the failed count goes up by 1 and the customer stays on S2 (BR-04).

**E6: Wrong code, third time (step 7).** The code is invalidated, the account is locked for 30 minutes if it exists, and the customer sees M-04. The flow ends (BR-04).

**E7: Password rejected (step 10).** The customer sees M-07 and stays on S3 (BR-06).

**E8: Code not verified (step 10).** A password arrives for an attempt whose code was never accepted. The customer returns to S2 with M-02 and nothing changes (BR-06).

### Postconditions

**Success:** The password is replaced, all sessions have ended, a confirmation SMS is sent and the attempt is COMPLETED.  
**Failure:** The password is unchanged. After E6 the account is locked for 30 minutes.

---

## What this use case leaves out

It names the Auth Service, the OTP Service and the SMS Gateway as actors without showing who waits for whom, which `bpmn.md` draws. It also refers to messages by ID only. The wording sits in `wireframe.md`.

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
