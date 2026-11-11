# 015 · Isolation Levels and Read Anomalies

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Two doctors each see the other on call and both remove themselves, leaving nobody on duty.

## Prerequisites

Before this session, review: [014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md); concurrent transactions, database snapshots.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Why can individually valid transactions violate a shared rule?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Isolation controls what concurrent transactions may observe and which conflicts cause aborts. Under snapshot isolation, transactions can read the same old snapshot and update different rows, producing write skew. Protect the shared invariant with an appropriate lock strategy, schema constraint when expressible, or serializable isolation with whole-transaction retries. Names and exact behavior differ by database, so verify the implementation rather than assuming a universal table.

## Trade-offs and limits

Stronger isolation can prevent anomalies but introduces blocking or retries. Read-only reporting may need a stable snapshot without requiring every write to serialize.

</details>

## Failure exercise

Run both on-call removals concurrently and inspect the final count under the chosen isolation level.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write the two-transaction timeline and identify a shared lock target that protects the rule. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md) · [Next: 016](../../designs/02-data-and-storage/016-optimistic-and-pessimistic-concurrency.md)
