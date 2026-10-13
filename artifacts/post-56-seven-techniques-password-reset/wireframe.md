# Wireframe: Password Reset by OTP

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Shows what the customer sees on each screen and the exact text of every message. Reach for it when product or design needs to agree on wording before anything is built, and when someone has to decide what the screen says in the cases a customer never sees on the happy path.

---

## Screens

Field names in the boxes are the same names used in `data-mapping.md`. Message slots in brackets show where a message lands, and the table below holds the text.

**S1: Request a code**

```
+------------------------------------------------+
|  Reset your password                           |
|                                                |
|  Mobile number                                 |
|  +------------------------------------------+  |
|  | mobile_number                            |  |
|  +------------------------------------------+  |
|                                                |
|  [ Send code ]                                 |
|                                                |
|  Back to sign in                               |
|                                                |
|  (M-05 or M-06 appears here when refused)      |
+------------------------------------------------+
```

**S2: Enter the code**

```
+------------------------------------------------+
|  Enter your code                               |
|                                                |
|  (M-01 appears here)                           |
|                                                |
|  6-digit code                                  |
|  +------------------------------------------+  |
|  | otp_code                                 |  |
|  +------------------------------------------+  |
|                                                |
|  (M-02, M-03 or M-04 appears here)             |
|                                                |
|  [ Verify ]                                    |
|                                                |
|  Resend code (60 second wait)                  |
+------------------------------------------------+
```

**S3: Choose a new password**

```
+------------------------------------------------+
|  Choose a new password                         |
|                                                |
|  New password                                  |
|  +------------------------------------------+  |
|  | new_password                             |  |
|  +------------------------------------------+  |
|  Confirm password                              |
|  +------------------------------------------+  |
|  | confirm_password                         |  |
|  +------------------------------------------+  |
|                                                |
|  (M-03 or M-07 appears here)                   |
|                                                |
|  [ Save password ]                             |
+------------------------------------------------+
```

**S4: Done**

```
+------------------------------------------------+
|  Password changed                              |
|                                                |
|  (M-08 appears here)                           |
|                                                |
|  [ Sign in ]                                   |
+------------------------------------------------+
```

---

## Messages

| ID | Screen | Shown when | Text | Rule |
|---|---|---|---|---|
| M-01 | S2 | After every request that is not refused | If this number belongs to an account, we sent a 6-digit code. It is valid for 5 minutes. | BR-03, BR-08 |
| M-02 | S2 | Wrong code, first or second time, or a password sent before the code was verified | That code is not correct. Check it and try again. | BR-04 |
| M-03 | S2, S3 | The attempt is older than 5 minutes | That code has expired. Request a new one. | BR-03 |
| M-04 | S2 | Third wrong code | Too many incorrect codes. Try again in 30 minutes. | BR-04, BR-08 |
| M-05 | S1 | 3 requests already in the past hour | Too many requests. Try again later. | BR-05 |
| M-06 | S1, S2 | Under 60 seconds since the last request | Please wait 60 seconds before requesting a new code. | BR-05 |
| M-07 | S3 | The new password fails BR-06 | Use at least 12 characters and choose a password different from your current one. | BR-06 |
| M-08 | S4 | The reset is complete | Your password was changed. Sign in with your new password. | BR-07 |

---

## What this wireframe leaves out

It shows the screen and says nothing about the account behind it. Whether the number is registered, whether the account is locked and what gets stored all sit in `use-case.md` and `data-mapping.md`. The wireframe's own contribution is M-01, M-02 and M-04: three messages that read the same for a registered and an unregistered number (BR-08).

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
