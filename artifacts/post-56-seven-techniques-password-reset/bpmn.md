# Process Flow: Password Reset by OTP

**Series:** Systems Analyst Notes  
**Post:** 56  
**Phase:** 7 Process, Compliance and Fintech Reality  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Draws the reset as a BPMN-style flow across four swim lanes, so the hand-offs between systems are visible. Reach for it when Ops or an integration owner needs to see which system acts at each step and where the customer is left waiting.

---

## How to read it

Mermaid has no BPMN notation, so the diagram borrows the shapes. Each swim lane is a subgraph, a diamond is an exclusive gateway, and a rounded shape is a start or end event. Rule IDs sit inside the gateway they govern.

One path is missing on purpose. When the SMS Gateway rejects a message (E3 in `use-case.md`), the failure is logged and the customer sees nothing different, so it has no branch here.

---

## Diagram

```mermaid
flowchart LR
    subgraph L1["Customer"]
        C1(["Taps Forgot password"])
        C2["Enters mobile number"]
        C3["Enters code"]
        C4["Enters new password"]
        C5(["Signs in with new password"])
        C6(["Request refused"])
        C7(["Locked for 30 minutes"])
    end

    subgraph L2["Auth Service"]
        A1{"Limits met? BR-05"}
        A2["Create reset attempt"]
        A3{"Account usable?"}
        A4["Show M-01 and code screen"]
        A5{"Within 5 minutes? BR-03"}
        A6{"Code matches?"}
        A7{"Third failure? BR-04"}
        A8["Show M-02, count failure"]
        A9["Show M-03"]
        A10["Show M-04, lock account if it exists"]
        A11{"Within 5 minutes? BR-03"}
        A12{"Password meets BR-06?"}
        A13["Replace password, end all sessions"]
        A14["Show S4 with M-08"]
    end

    subgraph L3["OTP Service"]
        O1["Generate code, store hash, set 5 minute expiry"]
        O2["Compare code with stored hash"]
    end

    subgraph L4["SMS Gateway"]
        G1["Deliver code by SMS"]
        G2["Deliver confirmation SMS"]
    end

    C1 --> C2
    C2 --> A1
    A1 -->|"No: M-05 or M-06"| C6
    A1 -->|"Yes"| A2
    A2 --> A3
    A3 -->|"Yes"| O1
    O1 --> G1
    G1 --> A4
    A3 -->|"No: no SMS sent"| A4
    A4 --> C3
    C3 --> A5
    A5 -->|"No"| A9
    A5 -->|"Yes"| O2
    O2 --> A6
    A6 -->|"Yes"| C4
    A6 -->|"No"| A7
    A7 -->|"No"| A8
    A8 --> C3
    A7 -->|"Yes"| A10
    A10 --> C7
    C4 --> A11
    A11 -->|"No"| A9
    A11 -->|"Yes"| A12
    A12 -->|"No: M-07"| C4
    A12 -->|"Yes"| A13
    A13 --> G2
    A13 --> A14
    A14 --> C5
    A9 -->|"Resend"| A1
```

---

## What this diagram leaves out

It shows who acts and in what order, and nothing about what the customer reads or what gets stored. Message wording sits in `wireframe.md`, and field-level storage in `data-mapping.md`.

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
