<!-- LinkedIn: -->

# C4 Level 2: Container Diagram for a Cross-Border Payment Platform

**Series:** Systems Analyst Notes  
**Post:** 49  
**Phase:** 6 AI Agents at Work  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Opens the Payment Platform box into the eight separately running parts that make it work, with the technology and the labeled relationships between them. Reach for it when someone asks what runs where, or what a change to one service touches.

---

## Diagram

```mermaid
C4Container
    title Container Diagram: Payment Platform

    Person(customer, "Customer", "Submits payments and follows their status")

    System_Boundary(platform, "Payment Platform") {
        Container(app, "Client App", "Mobile app", "Collects the instruction and shows status")
        Container(gateway, "API Gateway", "REST/JSON", "Authenticates and routes requests")
        Container(orch, "Payment Orchestrator", "Service", "Owns the payment flow and its status")
        ContainerDb(db, "Payments DB", "Relational database", "Stores instructions, status and idempotency keys")
        ContainerQueue(broker, "Event Broker", "Message broker", "Carries payment events to consumers")
        Container(screening, "Screening Service", "Service", "Checks debtor and creditor against watchlists")
        Container(ledger, "Ledger Adapter", "Service", "Reserves and posts funds in core banking")
        Container(notify, "Notification Service", "Service", "Sends status advices and beneficiary notices")
    }

    System_Ext(kyc, "KYC Provider", "Verifies customer identity")
    System_Ext(core, "Core Banking", "Holds accounts, reserves and posts funds")
    System_Ext(sanctions, "Sanctions Provider", "Supplies watchlist data for screening")
    System_Ext(corr, "Correspondent Bank", "Receives settlement instructions and returns status")
    System_Ext(audit, "Compliance Audit Log", "Keeps the record of every event that needs a paper trail")

    Rel(customer, app, "Uses", "Mobile UI")
    Rel(app, gateway, "Submits payments and polls status", "HTTPS, JSON")
    Rel(gateway, orch, "Forwards authenticated requests", "REST/JSON")
    Rel(orch, db, "Reads and writes payment state", "SQL")
    Rel(orch, screening, "Requests screening of both parties", "REST/JSON, 3s timeout")
    Rel(orch, ledger, "Reserves funds", "REST/JSON")
    Rel(orch, corr, "Sends settlement instructions, receives status", "ISO 20022 MX")
    Rel(orch, kyc, "Checks verification status", "HTTPS, JSON")
    Rel(orch, broker, "Publishes payment events", "Messages")
    Rel(broker, notify, "Delivers settlement events", "Messages")
    Rel(broker, audit, "Streams auditable events", "Event feed")
    Rel(screening, sanctions, "Pulls watchlist data", "Scheduled sync")
    Rel(ledger, core, "Reserves and posts funds", "Core banking API")
    Rel(notify, customer, "Sends status advices", "Push, email")

    UpdateElementStyle(orch, $bgColor="#1B2A4A", $fontColor="#FFFFFF", $borderColor="#1B2A4A")
    UpdateLayoutConfig($c4ShapeInRow="4", $c4BoundaryInRow="1")
```

## What this level shows

The parts that run on their own inside one system. A container here has nothing to do with Docker. It is a mobile app, an API, a message broker, a database: anything that executes code or holds state separately from the rest.

The orchestrator sits at the center because every other container talks to it or through it. That makes it the box to open next, and it is the one `component.md` zooms into.

Every box carries a name, a type, a technology and one line of description. A box that says "Service" and nothing else is a placeholder.

## How to adapt it

**Step 1: List what runs separately, one box each.** Include databases, brokers and queues. Leave out libraries and classes, which belong one level down.

**Step 2: Write the technology on every box.** If nobody on the team can say what a box is built with, that is a finding.

**Step 3: Label each line with a verb and a protocol.** Add timeouts where a failure would stall the payment, the way the screening line does here.

**Step 4: Check that nothing from level 3 leaked in.** A controller or a class on this diagram means two zoom levels are mixed, which is the failure C4 exists to prevent.

---

## Related Artifacts

* [artifacts/post-49-c4-diagrams/context.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-49-c4-diagrams/context.md) - Level 1, the boundary this diagram opens
* [artifacts/post-49-c4-diagrams/component.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-49-c4-diagrams/component.md) - Level 3, which opens the Payment Orchestrator box
* [artifacts/post-21-requirement-decomposition-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-21-requirement-decomposition-template.md) - Names an owner for each container before requirements are split
* [artifacts/post-25-sequence-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.md) - Shows the order of the calls drawn here as unordered lines

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
