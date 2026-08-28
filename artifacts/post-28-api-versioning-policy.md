<!-- LinkedIn: https://lnkd.in/p/gx-Xchib-->

# API Versioning and Deprecation Policy

**Series:** Systems Analyst Notes  
**Post:** 28  
**Phase:** 4 APIs as Products  
**Author:** Yulia Melekhova  
**Published:** 2026

## Purpose

Settles what counts as a breaking change before a change is proposed, and fixes the notice a client gets when one ships. Fill in the four bracketed values once per API, publish it where clients can read it, and cite it in review instead of relitigating it.

---

## 1. Scope

This policy covers one API surface. Where an organization runs several with different audiences, each gets its own filled copy, because the notice period an internal consumer needs and the notice period a licensed partner needs are different numbers.

Four values are decided once and appear throughout. Everything else in this file is fixed text.

| Value | Written as | Set by |
|---|---|---|
| Current major version | `[CURRENT_VERSION]` | API owner |
| Standard notice period | `[NOTICE_DAYS]` days | API owner with commercial input |
| Extended notice period for external clients | `[EXTENDED_NOTICE_DAYS]` days | Commercial owner |
| Deprecation contact | `[DEPRECATION_CONTACT]` | API owner |

---

## 2. The version identifier

The version is carried in the URL path as `/v[N]/`, and the full build identifier is returned in every response as the `API-Version` header in the form `[N].[MINOR].[PATCH]`.

The path segment tells a client which contract it is talking to. The header tells support which build produced a specific response, which is the question that gets asked during an incident and cannot be answered from the path alone.

Payment message identifiers are the reference model here, and they are stricter than most APIs need to be. `pacs.008.001.08` names the business area, the message, the variant and the version in one string, so a consumer resolves the schema before parsing a field. The property worth copying is not the format. It is that a field cannot change without the identifier changing with it.

---

## 3. What counts as breaking

A change is breaking when a client that was working correctly against the published contract can stop working correctly without changing its own code.

| Change | Breaking | Why |
|---|---|---|
| Remove a field from a response | Yes | A client reading it gets nothing, or a parse error |
| Rename a field in a request or a response | Yes | Equivalent to a removal plus an addition, and worse because it looks cosmetic |
| Add a required field to a request | Yes | Every existing caller is now sending an invalid request |
| Narrow a type, tighten a format, or shorten a maximum length | Yes | Values that were valid yesterday are rejected today |
| Guarantee that an optional response field is always present | No | A reader that already handles the field is unaffected |
| Change the meaning of an existing value | Yes | Nothing in the schema moves and no validator complains |
| Change a default value | Yes | Callers relying on the old default silently get different behavior |
| Change the order of a paginated result set without a new parameter | Yes | Pagination becomes non-deterministic across pages |
| Add a new error code inside an existing HTTP status | Depends | See section 4 |
| Remove an endpoint | Yes | The obvious one, and the one already handled well by most teams |

**The semantic change is the one that gets missed.** A status value that used to mean "accepted by us" and now means "accepted by the correspondent" carries the same name, the same type and the same length. Every client keeps parsing it successfully into a wrong answer. Schema diff tooling will not catch this class of change, which is why it needs a human question in review: does any value in this response mean something different than it did last week?

---

## 4. The cases that have to be decided, not assumed

Three changes are breaking or not depending on what the API told its clients to do. Decide each one when the policy is first published, and record the decision here rather than in a review thread.

**Adding a new enum value to a response.** Harmless for a client that ignores values it does not recognize. Fatal for a client that validates strictly against a generated model. Decide by stating the client obligation in the contract: *clients must tolerate unknown values in `[FIELD_LIST]` and treat them as `UNKNOWN`.* Once that sentence is published, adding a value is non-breaking. Without it, it is breaking.

**Adding a new optional field to a response.** Non-breaking under the same tolerance rule. Breaking for any client using strict schema validation with `additionalProperties: false`.

**Loosening a validation rule on a request.** Non-breaking for callers, and breaking for anything downstream that assumed the tighter rule held. Trace the field to its consumers before classifying it.

---

## 5. Deprecation timeline

Five stages, each with an owner and an artifact. A stage without an artifact has not happened.

**Stage 1: Decision.** The API owner records the deprecation as an ADR, naming the replacement, the reason and the migration path. No client is told anything yet, because a deprecation announced without a migration path generates support load and no migrations.

**Stage 2: Announcement.** Day 0. The replacement is live and documented. Clients are notified through the release notes, the changelog and a direct message to every registered integrator. The sunset date is stated as a date, never as a quarter.

**Stage 3: Signaling.** From day 0 until the sunset date, every response from the deprecated surface carries the headers in section 6. This is what reaches the engineer who never reads release notes.

**Stage 4: Reminders.** At 50% of the notice period, at 30 days remaining and at 7 days remaining, the remaining callers are contacted individually. By this stage the traffic logs name them, so the message goes to the clients that actually still call rather than to a mailing list.

**Stage 5: Sunset.** The endpoint returns `410 Gone` with a body naming the replacement and `[DEPRECATION_CONTACT]`. It is not removed from the routing table for a further 30 days, because a `410` with an explanation resolves a support ticket and a `404` creates one.

### Notice period by client tier

| Client tier | Notice period | Runs from |
|---|---|---|
| Internal service in the same delivery org | `[NOTICE_DAYS]` days | Announcement |
| External integrator, no contractual commitment | `[EXTENDED_NOTICE_DAYS]` days | Announcement |
| External integrator with a contractual notice term | Whichever is longer, the contract term or `[EXTENDED_NOTICE_DAYS]` days | Announcement |
| Any client where the change is mandated externally | The mandate date, minus the migration estimate | The date the mandate was published |

The last row is the one that breaks the pattern. When a regulator or a network sets the date, the notice period is not a decision the API owner makes. It is the residue left after the external date and the internal migration estimate are subtracted from each other, and it is sometimes negative. Discovering that early is the whole reason the row exists.

---

## 6. Sunset signaling

Every response from a deprecated surface carries three headers, from the announcement until the sunset date.

```
Deprecation: Fri, 14 Nov 2026 00:00:00 GMT
Sunset: Sat, 13 Feb 2027 00:00:00 GMT
Link: <https://docs.example.com/migrations/v2-to-v3>; rel="deprecation"
```

`Deprecation` carries the announcement date. `Sunset` carries the date the surface stops answering. `Link` points at the migration guide, not at the API documentation root, because a client that has just discovered the header needs the diff and not the index.

Log every request that arrives with a deprecated path after the announcement, tagged with the client identifier. That log is the reminder list in stage 4 and the evidence in any argument about whether a client was told.

---

## 7. What the client is promised

A versioning policy is a promise in both directions. Two obligations belong to the API owner and two belong to the client, and stating all four is what makes the policy enforceable rather than aspirational.

The API owner will not make a breaking change inside a published major version, will give at least the notice period in section 5, will keep the previous major version answering for the full notice period, and will publish a migration guide before the announcement rather than after it.

The client will tolerate unknown enum values and unknown response fields, will not depend on undocumented behavior, will keep a working contact address on file for deprecation notices, and will act on a `Sunset` header rather than waiting for an account manager to call.

---

## 8. Review gate

Five checks before any change to a published API merges. All of them are cheap, and the third is the one that catches what tooling misses.

1. Has the change been classified as breaking or non-breaking against section 3, with the classification written in the pull request rather than assumed?
2. If breaking, does a new major version exist, and is the previous one still answering?
3. Does any value in a response mean something different than it did before this change, while keeping its name, type and length?
4. Is the changelog row written, using the five columns from the Post 24 template, including what else had to change?
5. If a deprecation starts here, are the headers in section 6 present in the response and is the sunset date a real date?

A change that fails check 3 is the one that ships successfully, passes every test and produces a support case eight weeks later that nobody connects back to this release.

---

## Related Artifacts

* [artifacts/post-22-api-contract-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-22-api-contract-template.yaml) - The contract this policy versions, and where the field definitions being classified live
* [artifacts/post-24-changelog-template.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-24-changelog-template.md) - The five columns referenced by check 4 in the review gate
* [artifacts/post-23-adr-template.yaml](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-23-adr-template.yaml) - Where a deprecation decision is recorded at stage 1, before any client hears about it
* [artifacts/post-25-sequence-diagram.md](https://github.com/YuliaMelekhova/systems-analyst-notes/blob/main/artifacts/post-25-sequence-diagram.md) - Shows which participants a versioned response reaches, which is how the client tier list gets built

---

Systems Analyst Notes · [github.com/YuliaMelekhova/systems-analyst-notes](https://github.com/YuliaMelekhova/systems-analyst-notes)

LinkedIn · https://www.linkedin.com/in/yuliamelekhova
