# 052 · Consistency Models and User Guarantees

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A user edits a profile and immediately reads an older version from another replica.

## Prerequisites

Before this session, review: [014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md),[051](../../designs/06-distributed-systems/051-replication-and-failover.md); concurrent operations, replicas.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Is eventual convergence enough for this user journey?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Specify observable guarantees per operation. Read-your-writes can route the session to an up-to-date replica or carry a version token. Linearizability makes each operation appear atomic between invocation and response; eventual consistency promises convergence under suitable conditions after updates stop. Transaction isolation and replica consistency describe different aspects. Name the needed behavior instead of calling the whole system simply consistent.

## Trade-offs and limits

Stronger guarantees usually require coordination and can increase latency or reject operations during failures. Some display data tolerates lag; ownership and money rules often need stronger checks.

</details>

## Failure exercise

Write through one instance and read through another while introducing replication lag.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Choose consistency guarantees for profile edits, product counts, and seat ownership. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 051](../../designs/06-distributed-systems/051-replication-and-failover.md) · [Next: 053](../../designs/06-distributed-systems/053-network-partitions-and-cap-tradeoffs.md)
