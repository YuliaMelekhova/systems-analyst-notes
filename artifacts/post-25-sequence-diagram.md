<!-- LinkedIn: -->

# Cross-Service Payment Sequence

**Series:** Systems Analyst Notes  
**Post:** 25  
**Phase:** 4 APIs as Products  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

Draws one payment instruction as a timed conversation between six services, with the branches, the waiting, the timeouts and the duplicate submission shown rather than described. Reach for it when a prose flow description has stopped answering questions about ordering.

---

## How to Adapt It

Rename the participants to your own services and keep four things: the alt branches, the timeout notes on the arrows that leave your boundary, the idempotency key on every retry, and the async confirmation that arrives from a participant nobody called.

```mermaid
sequenceDiagram
    autonumber
    actor CUST as Customer
    participant APP as Client App
    participant ORC as Payment Orchestrator
    participant SCR as Sanctions Screening
    participant CORE as Core Banking
    participant CORR as Correspondent Bank
    participant NTF as Notification Service

    CUST->>APP: Submit payment instruction
    APP->>ORC: POST /payments (Idempotency-Key)
    Note right of APP: Timeout 8s, 2 retries, exponential backoff.<br/>Same Idempotency-Key on every attempt.
    ORC->>ORC: Persist instruction, status = received
    ORC-->>APP: 202 Accepted (paymentId)
    APP-->>CUST: Payment submitted

    ORC->>SCR: Screen debtor and creditor
    Note right of SCR: Timeout 3s. On timeout the payment holds.<br/>It is never cleared automatically.

    alt Screening returns clear
        SCR-->>ORC: clear
        ORC->>CORE: Reserve funds
        alt Funds reserved
            CORE-->>ORC: reserved (reservationId)
            ORC->>CORR: Send settlement instruction
            CORR-->>ORC: accepted (status ACSP)
            ORC->>ORC: status = sent
        else Insufficient funds
            CORE-->>ORC: rejected (reason AC04)
            ORC->>ORC: status = failed, reason recorded
        end
    else Screening returns a hit
        SCR-->>ORC: hit (caseId)
        ORC->>ORC: status = compliance hold
        Note over ORC,SCR: Manual review, no SLA the customer can see.<br/>What the app shows meanwhile is a requirement, not a detail.
    else Screening does not answer
        SCR--xORC: no response within 3s
        ORC->>ORC: status = screening pending, retry scheduled
    end

    opt Client timed out and resubmitted
        APP->>ORC: POST /payments (same Idempotency-Key)
        ORC-->>APP: 200 OK (original paymentId, no second payment created)
    end

    CORR--)ORC: Settlement confirmation (async, minutes to hours)
    ORC->>NTF: Publish payment.settled
    NTF--)CUST: Beneficiary notification

    opt Settlement confirmation never arrives
        Note over ORC,CORR: Investigation raised. The owner, the deadline and the<br/>message shown to the customer all belong in the spec.
    end
```

---

## Related Artifacts

* [artifacts/post-16-context-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-16-context-diagram.md) - Draws the boundary these arrows cross, before the ordering matters
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - Where the alt branches in this diagram come from
* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - The contract each arrow is calling, including the timeout and retry fields annotated here
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Names the owner of every participant on this diagram before the conversation is specified
* [artifacts/post-28-api-versioning-policy.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-28-api-versioning-policy.md) - How this same participant list turns into a notice period and a breaking-change classification

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
