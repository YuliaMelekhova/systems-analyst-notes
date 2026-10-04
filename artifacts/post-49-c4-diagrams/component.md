<!-- LinkedIn: -->

# C4 Level 3: Component Diagram for the Payment Orchestrator

**Series:** Systems Analyst Notes  
**Post:** 49  
**Phase:** 6 AI Agents at Work  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Opens one container, the Payment Orchestrator, into the eight components that carry its behavior. Reach for it when a rule such as idempotency, screening timeouts or status ownership needs a named place to live before anyone writes the spec.

---

## Diagram

```mermaid
flowchart LR
    gateway["<b>API Gateway</b><br/>[Container: REST/JSON]"]

    subgraph orch["Payment Orchestrator [container boundary]"]
        ctrl["<b>Controller</b><br/>[Component: REST controller]<br/>Receives POST /payments,<br/>answers 202 with a paymentId"]
        idem["<b>Idempotency Handler</b><br/>[Component]<br/>A repeated key returns<br/>the original paymentId"]
        valid["<b>Validator</b><br/>[Component]<br/>Checks schema, limits and<br/>corridor rules"]
        fsm["<b>State Machine</b><br/>[Component]<br/>Owns status from received<br/>to settled, held or failed"]
        scrcl["<b>Screening Client</b><br/>[Component: HTTP client]<br/>Holds on timeout,<br/>never clears automatically"]
        ledcl["<b>Ledger Client</b><br/>[Component: HTTP client]<br/>Requests the reservation,<br/>records the reservation id"]
        setcl["<b>Settlement Client</b><br/>[Component: ISO 20022]<br/>Builds the instruction,<br/>reads status messages"]
        pub["<b>Event Publisher</b><br/>[Component]<br/>Emits events such as<br/>payment.settled"]
    end

    db[("<b>Payments DB</b><br/>[Container]")]
    screening["<b>Screening Service</b><br/>[Container]"]
    ledger["<b>Ledger Adapter</b><br/>[Container]"]
    corr["<b>Correspondent Bank</b><br/>[External System]"]
    broker[["<b>Event Broker</b><br/>[Container]"]]

    gateway -->|"Forwards requests<br/>[REST/JSON]"| ctrl
    ctrl -->|"Checks the key first"| idem
    ctrl -->|"Validates the instruction"| valid
    ctrl -->|"Creates payment<br/>as received"| fsm
    fsm ---->|"Persists status<br/>[SQL]"| db
    fsm -->|"Requests screening"| scrcl
    fsm -->|"Requests reservation"| ledcl
    fsm -->|"Requests settlement"| setcl
    fsm -->|"Emits events"| pub
    scrcl -->|"Screens both parties<br/>[REST/JSON, 3s timeout]"| screening
    ledcl -->|"Reserves funds<br/>[REST/JSON]"| ledger
    setcl -->|"Sends instruction,<br/>receives status<br/>[ISO 20022 MX]"| corr
    pub -->|"Publishes events<br/>[Messages]"| broker

    classDef box fill:#FFFFFF,stroke:#5B6B84,color:#1B2A4A
    classDef rust fill:#C1502E,stroke:#C1502E,color:#FFFFFF
    classDef ext fill:#F5F1E8,stroke:#5B6B84,color:#1B2A4A
    class ctrl,valid,fsm,scrcl,ledcl,setcl,pub box
    class idem rust
    class gateway,db,screening,ledger,broker,corr ext
    style orch fill:none,stroke:#5B6B84,stroke-dasharray:6 4
```

**Notation:** Drawn as a Mermaid flowchart that follows C4 conventions: every box carries a name, a type and a description, and every line a verb and a protocol. Mermaid's native C4 syntax is not used because its automatic layout puts labels on top of lines once a diagram passes a handful of relationships.

## What this level shows

The building blocks inside one container, grouped by responsibility rather than by class name. Only the neighbors that the orchestrator actually calls appear outside the boundary.

The idempotency handler is highlighted because it is where the sequence diagram's duplicate-submission question gets its answer. The same Idempotency-Key arriving twice returns the original paymentId and creates no second payment. Before this diagram, that rule lived in a note on an arrow. Now it has an address, an owner and a place for a test.

Level 4, the classes and tables behind each component, is deliberately missing. Generate it from the codebase when someone needs it. A hand-drawn version is wrong within a sprint.

## How to adapt it

**Step 1: Pick one container to open.** Choose the one where most rules live, usually the one every other container talks to.

**Step 2: List its components by responsibility.** "Idempotency Handler" is a responsibility. "PaymentServiceImpl" is a class.

**Step 3: Show only what crosses the container boundary.** Draw the neighbors this container calls and nothing further away.

**Step 4: Stop here unless a component's behavior is disputed.** If it is, draw a sequence diagram for that one component rather than a level 4 diagram.

---

## Related Artifacts

* [artifacts/post-49-c4-diagrams/container.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-49-c4-diagrams/container.md) - Level 2, where the Payment Orchestrator box comes from
* [artifacts/post-25-sequence-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.md) - The timeouts and retries annotated on its arrows are the rules these components carry
* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - The contract behind the Controller and the Settlement Client
* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - Where the decision to hold on a screening timeout gets recorded

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova

