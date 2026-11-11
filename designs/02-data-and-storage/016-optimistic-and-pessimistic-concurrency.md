# 016 · Optimistic and Pessimistic Concurrency

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A sale has one item left and two buyers click at the same time.

## Prerequisites

Before this session, review: [014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md)–[015](../../designs/02-data-and-storage/015-isolation-levels-and-read-anomalies.md); versions, row locks.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Is checking stock before a separate decrement safe?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use an atomic conditional update that decrements stock only where stock is positive, then inspect the affected-row count. For more complex logic, acquire a database row lock and keep the transaction short. Optimistic version checks detect stale writers; pessimistic locks make contenders wait. Adopt a consistent lock order for multi-row changes and handle deadlocks by retrying the whole transaction safely.

## Concrete example

Illustrative SQL; adapt parameters and verify database behavior before use.

```sql
-- Illustrative PostgreSQL-style statement inside the business transaction.
UPDATE inventory
SET available = available - 1
WHERE sku = :sku AND available > 0
RETURNING sku, available;
-- No returned row means no reservation was made.
```

## Trade-offs and limits

Optimistic control avoids waiting when conflicts are rare. Under heavy contention repeated retries waste work; locks can help but increase wait times and require limits.

</details>

## Failure exercise

Launch two reservations for stock 1. One succeeds and the final stock is 0, never negative.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Compare version checks, conditional decrements, and row locking for a shared inventory record. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 015](../../designs/02-data-and-storage/015-isolation-levels-and-read-anomalies.md) · [Next: 017](../../designs/02-data-and-storage/017-schema-migrations-without-downtime.md)
