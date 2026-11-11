# 076 · Audit Trails and Tamper Evidence

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

An administrator changes permissions and later removes the evidence.

## Prerequisites

Before this session, review: [014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md),[061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md),[071](../../designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md); actor identity, immutable history.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Who can alter the audit trail itself?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Record actor, action, target, outcome, time, and correlation identifiers using trusted context. Protect the audit destination with separate permissions and retention controls. For stronger evidence, use append-only storage, chained hashes, or signed checkpoints with externally protected anchors as appropriate. A hash chain alone does not prevent an attacker who can rewrite the entire chain. Avoid recording secrets.

## Trade-offs and limits

Detailed auditing supports investigation but increases sensitive-data retention and access-control requirements. Decide whether an audit failure blocks critical actions or enters a recoverable path.

</details>

## Failure exercise

Attempt modification with the normal application identity and verify detection or prevention.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design an audit event for a role change and specify the permissions of writers and reviewers. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 075](../../designs/08-security-and-multi-tenancy/075-encryption-and-data-protection-boundaries.md) · [Next: 077](../../designs/08-security-and-multi-tenancy/077-input-trust-boundaries-and-ssrf-defense.md)
