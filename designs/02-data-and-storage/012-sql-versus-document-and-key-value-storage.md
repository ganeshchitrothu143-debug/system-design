# 012 · SQL versus Document and Key Value Storage

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A team chooses a database based on popularity before listing its queries.

## Prerequisites

Before this session, review: [011](../../designs/02-data-and-storage/011-relational-data-modeling.md); keys, access patterns, transactions.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What transaction or lookup would become difficult with your chosen model?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

List writes, reads, consistency needs, growth, and operational constraints first. Relational storage suits relationships and multi-row constraints. Documents can group data commonly read together, but large or unbounded embedded arrays create problems. Key-value storage makes direct key access simple while secondary queries may need extra indexes or projections. Evaluate the actual product's transaction and indexing behavior; SQL and NoSQL labels alone do not define guarantees.

## Trade-offs and limits

One general database can reduce operational burden. Multiple specialized stores may improve particular workloads but add synchronization, backups, and failure modes.

</details>

## Failure exercise

Try the three most important queries and one cross-record invariant on each candidate model.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Compare storing shopping carts as relational rows versus one document per cart. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 011](../../designs/02-data-and-storage/011-relational-data-modeling.md) · [Next: 013](../../designs/02-data-and-storage/013-indexes-and-query-access-paths.md)
