# 044 · Idempotency Keys and Duplicate Requests

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A client retries checkout after losing the response and creates two orders.

## Prerequisites

Before this session, review: [014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md),[041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md)–[043](../../designs/05-jobs-and-events/043-retries-backoff-and-jitter.md); unique constraints, operation IDs.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What if the same key arrives with a different request body?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Scope an idempotency key to the actor and operation. Persist the key, request fingerprint, operation state, and result under a uniqueness constraint. Concurrent duplicates must converge on the same operation. Reject key reuse with a different payload. Commit the business effect and key state atomically when both live in one database; external effects need their own idempotency or reconciliation. Define retention and in-progress response behavior.

## Concrete example

Illustrative pseudocode or contract, not a complete implementation.

```text
operation_key = (authenticated_actor, operation_type, idempotency_key)
atomically claim operation_key using a unique constraint
if existing fingerprint differs: reject key reuse
if completed: return stored result
if running: return documented in-progress response
otherwise: perform and record recoverable operation
```

## Trade-offs and limits

Storing results costs space and key expiry limits how long duplicates are recognized. An in-memory lookup is insufficient across crashes or multiple instances.

</details>

## Failure exercise

Submit the same key concurrently, lose the first response, and retry after restart.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design the idempotency record and response behavior for new, in-progress, completed, and conflicting requests. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 043](../../designs/05-jobs-and-events/043-retries-backoff-and-jitter.md) · [Next: 045](../../designs/05-jobs-and-events/045-dead-letter-queues-and-safe-replay.md)
