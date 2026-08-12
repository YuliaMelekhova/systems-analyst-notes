# Requirement and ADR Antipatterns

**Series:** Systems Analyst Notes  
**Branch:** Templates and Quality Rules  
**Author:** Yulia Melekhova  
**Published:** 2026  

## Purpose

The failures that clear every readiness gate, survive review, and break during integration or after go-live. Reach for it during a review pass, or after an incident traced back to a document that everyone had approved.

---

## Why the Opposite of a Template

Templates describe the shape of a correct artifact. They cannot describe the ways a correctly shaped artifact is still wrong, because those failures live in the content and the template has nothing to say about content.

Every entry below has been through a review and passed. That is the selection criterion. Requirements that obviously fail get caught, and the interesting failures are the ones that read well.

Each entry uses the same four parts: what it looks like, why review lets it through, what breaks, and what to write instead.

---

## Requirement Antipatterns

### The Passive Actor

**Looks like:** "The customer shall be notified when the payment settles."

**Passes because:** It has an actor, a trigger and an outcome. It reads like a requirement and parses like one.

**Breaks when:** Three services could plausibly send the notification and each assumes another one does. In the version where two of them do, the customer gets duplicate messages and files a complaint. In the version where none do, the gap shows up in a support ticket weeks later.

**Write instead:** Name the sender. "The payment orchestrator publishes a settlement event. The notification service consumes it and sends the customer message." Two sentences, one owner each, and the boundary between them is now testable.

### The Assumed Protocol

**Looks like:** "The system shall send SMS notifications to customers using the vendor API."

**Passes because:** The integration is named, the purpose is clear, and the sentence contains no ambiguity a reviewer can point at.

**Breaks when:** The developer reads it and assumes a POST request, a JSON payload, API key authentication and a synchronous response, because that is what most vendor APIs look like now. The actual vendor uses SOAP, XML, OAuth and an asynchronous webhook callback. None of the four assumptions hold, and the rework runs four weeks. That is a real number from a real integration, not an illustration.

**Write instead:** Attach the interface facts to the requirement. Transport, payload format, authentication method, response model, and what a failure looks like. If those are not known yet, the requirement is not ready and the readiness gate should have caught it. Two of the four are usually known, which is exactly why the gap survives review.

### The Unbounded Quantifier

**Looks like:** "All pending transactions are re-screened after a sanctions list update."

**Passes because:** The rule is clear and the intent is correct.

**Breaks when:** The list updates during a settlement window and `all pending` turns out to be six hundred thousand records. Nobody asked how large the set gets, because the sentence contains a word that made the set sound like a known quantity.

**Write instead:** Bound the set and state the timing. "Transactions in `pending_screening` status with a value date within the next five business days are re-screened within thirty minutes of a list update." Now capacity planning has an input, and the requirement can be load tested.

### The Single-Instance Requirement

**Looks like:** "When the client submits a payment, the system reserves the balance and returns a payment ID."

**Passes because:** It describes the flow correctly. Walked through by one reader, thinking about one payment, it is right.

**Breaks when:** Two submissions arrive within the same few milliseconds against the same balance. The requirement is silent on concurrency, so the implementation resolves it by accident and the resolution is discovered in production.

**Write instead:** State the concurrent case explicitly, even when the answer is boring. "Concurrent submissions against the same account serialize on the account balance. The second submission receives a rejection with reason `insufficient_available_balance` rather than queuing." Every requirement touching shared state needs one of these lines.

### Success-Only Specification

**Looks like:** A complete, well-structured requirement describing exactly what happens when everything works.

**Passes because:** Reviewers check whether what is written is correct. Checking for what is absent is a different cognitive task and a harder one.

**Breaks when:** The screening provider times out, and the implementation does whatever the framework's default does. Sometimes that is a retry. Sometimes it is proceeding without a verdict, which is a compliance failure created by a missing paragraph.

**Write instead:** Every external call gets a stated behavior for timeout, error response, and unexpected payload. Three lines per integration. The alternative is that a framework default becomes company policy without anyone deciding it.

### The Borrowed Threshold

**Looks like:** "Availability: 99.9%. Response time: under 200ms."

**Passes because:** It has numbers, and numbers look like rigor.

**Breaks when:** Someone asks what window the 99.9% is measured over, and there is no answer. Measured monthly, it allows a forty-three minute outage. If that outage lands inside a fixed settlement window in a cross-border corridor, the value for that window is lost permanently, and the SLA was met.

**Write instead:** Attach the measurement condition and the business consequence. "Availability 99.9% measured monthly, with no single outage exceeding fifteen minutes during settlement windows 09:00 to 11:00 and 14:00 to 16:00 local." The second clause is the one that matters, and it is the one borrowed thresholds never carry.

### The Reversible-Looking Irreversible Action

**Looks like:** "The user can update the beneficiary details on a submitted payment."

**Passes because:** Update is an ordinary word describing an ordinary operation.

**Breaks when:** The payment already left on the rail. What the requirement calls an update is a recall, a different process with a different cost, a different success rate and a different set of counterparties. The UI shipped with an edit button that cannot do what it promises.

**Write instead:** Split the requirement at the point of irreversibility. Before the message is sent, it is an update. After, it is a recall request with its own flow and its own failure states. Any requirement using update, cancel or delete near money movement needs this check.

### The Requirement That Specifies the Screen

**Looks like:** "A warning banner appears above the amount field when the amount exceeds the daily limit."

**Passes because:** It is specific, testable and easy to picture.

**Breaks when:** The same limit needs enforcing on the API, in the bulk file upload, and in the mobile app. The rule lives in one presentation layer, so it gets reimplemented twice more, and the three copies drift.

**Write instead:** Specify the rule and its enforcement point separately from the presentation. "The daily limit is evaluated at the orchestrator on every submission path. Rejection returns `daily_limit_exceeded`." The banner is then a presentation requirement referencing the rule, and there is one rule.

---

## ADR Antipatterns

### The Decision With No Alternatives

**Looks like:** A clean ADR stating the chosen approach with a clear rationale.

**Passes because:** The rationale is genuinely good.

**Breaks when:** Eighteen months later someone proposes the option that was already rejected. Nobody can say why it was rejected, because the record shows only what was chosen. The evaluation runs a second time, at full cost.

**Write instead:** At least two alternatives with the reason each was set aside. An ADR with no alternatives recorded a conclusion, not a decision.

### Consequences That Are All Benefits

**Looks like:** A consequences section listing what improves.

**Passes because:** The listed benefits are real and the reviewer agrees with them.

**Breaks when:** The cost shows up later and looks like a surprise rather than a known trade accepted with open eyes. Trust in the ADR set drops, because the team learns that the documents oversell.

**Write instead:** Costs in the same section, stated as plainly as the benefits. An ADR with no downside listed is either a decision that needed no ADR or an incomplete one.

### The ADR With No Revisit Trigger

**Looks like:** A well-reasoned decision that fits the current constraints.

**Passes because:** It does fit the current constraints. That is why it was made.

**Breaks when:** The constraint disappears and nobody notices. A choice made for a system handling two thousand payments a day survives to two hundred thousand because no condition was written down that would prompt a second look.

**Write instead:** Name the condition that invalidates the decision. "Revisit if daily volume exceeds fifty thousand, or if a second market is added." A decision with no expiry condition is being treated as permanent whether anyone intended that or not.

### The ADR Written After the Fact

**Looks like:** A complete ADR describing the architecture accurately.

**Passes because:** It is accurate. Everything in it is true.

**Breaks when:** It is used as evidence that a decision was deliberated. It documents an outcome, and the reasoning in it was assembled afterward to fit what already exists. Nobody can distinguish it from a real one, which quietly devalues every ADR in the set.

**Write instead:** Record it and label the timing honestly. `Status: accepted, recorded retrospectively` costs one line and preserves the meaning of the rest of the set.

### Context That Describes the System

**Looks like:** A context section explaining how the system works and where the component fits.

**Passes because:** It is informative, and a reader learns something from it.

**Breaks when:** A reader needs to know what made the decision hard. The context section describes the architecture, which they can already see, instead of the constraint that ruled out the obvious answer. Without the constraint, the decision looks arbitrary.

**Write instead:** Lead with the forcing constraint. Regulatory deadline, vendor limitation, a rule in an existing contract, a team boundary. Architecture is the setting. The constraint is the context.

### The Wrong Altitude

**Looks like:** A tidy ADR set covering library selections, framework versions and tooling choices.

**Passes because:** Each individual ADR is well written and each decision was real.

**Breaks when:** The decision that actually costs money to reverse is missing. Which service owns customer data. Whether payment state is authoritative in the ledger or the orchestrator. Those get made in a thread and never recorded, while the logging library gets three pages.

**Write instead:** Apply one test before writing. If reversing this in a year means a data migration, a contract renegotiation or a team reorganization, it needs an ADR. If reversing it means a pull request, it needs a comment.

---

## Using This in Review

Reading all fourteen before every review does not happen. Two questions cover most of the value.

**For a requirement: what happens when this fails, and what happens when two of these arrive at once?** Success-only specification and the single-instance requirement are the two most common entries here, and both are invisible until asked about directly.

**For an ADR: what was rejected, and what would make us change our minds?** Missing alternatives and missing revisit triggers account for most of the ADR set decay observed a year out.

---

## Related Artifacts

* [templates-quality-rules/readiness-rules.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/templates-quality-rules/readiness-rules.md) - The gates these failures pass through untouched
* [artifacts/post-19-unhappy-path-mapping.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-19-unhappy-path-mapping.md) - The method that catches success-only specification before review
* [stride-threat-modeling/payment-initiation-stride.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/stride-threat-modeling/payment-initiation-stride.md) - Several threats there exist only because a requirement had one of these shapes

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
