# 013 · Indexes and Query Access Paths

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Finding a customer's recent orders scans millions of rows.

## Prerequisites

Before this session, review: [011](../../designs/02-data-and-storage/011-relational-data-modeling.md)–[012](../../designs/02-data-and-storage/012-sql-versus-document-and-key-value-storage.md); filtering, ordering, basic SQL.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Why might an index on status alone fail to help this query?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Start from a concrete predicate and ordering: customer_id equality followed by created_at and id descending. A matching composite index can narrow the scan and supply order. Inspect the query plan and actual rows examined using realistic data. Index order, selectivity, covering columns, and database behavior matter. Every additional index consumes space and adds write work; measure before retaining it.

## Trade-offs and limits

Indexes accelerate selected reads, not every query. A low-selectivity filter may still favor a table scan. Too many indexes can make writes and migrations expensive.

</details>

## Failure exercise

Use both a small and very large customer account. Compare latency and rows examined rather than relying on one average.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Propose an index for recent orders per customer and explain what happens when sorting by total instead. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 012](../../designs/02-data-and-storage/012-sql-versus-document-and-key-value-storage.md) · [Next: 014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md)
