# 051 · Replication and Failover

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A primary database fails and the promoted replica is missing recent acknowledged writes.

## Prerequisites

Before this session, review: [014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md); primary and replica, replication logs, durable acknowledgments.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

When did the system promise that a write was durable?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Define the replication acknowledgment policy and recovery objectives. Asynchronous replicas may lag; synchronous replication can improve durability within its documented failure model at a latency and availability cost. Promotion must prevent the old primary from continuing as an independent writer. Route reads according to freshness needs and test how clients recover connections.

## Trade-offs and limits

Replication improves availability and read capacity but is not a backup against accidental deletion replicated everywhere. Failover guarantees depend on configuration and quorum behavior.

</details>

## Failure exercise

Write a known sequence, isolate the primary, promote a replica, and reconcile acknowledged records.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Compare asynchronous and synchronous acknowledgment for a catalog versus a financial ledger. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 050](../../designs/05-jobs-and-events/050-event-sourcing-and-projection-rebuilds.md) · [Next: 052](../../designs/06-distributed-systems/052-consistency-models-and-user-guarantees.md)
