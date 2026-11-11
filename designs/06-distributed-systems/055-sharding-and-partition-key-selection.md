# 055 · Sharding and Partition Key Selection

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

One database cannot hold the workload and the largest tenant dominates traffic.

## Prerequisites

Before this session, review: [013](../../designs/02-data-and-storage/013-indexes-and-query-access-paths.md),[022](../../designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md),[051](../../designs/06-distributed-systems/051-replication-and-failover.md); keys, distribution, cross-shard queries.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does evenly distributing rows also evenly distribute load?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Choose a shard key from access patterns, write distribution, and transaction boundaries. Tenant-based sharding simplifies tenant-local operations but creates hot-tenant risk. Hashing spreads keys while range partitioning can support scans; each complicates different queries. Maintain routing metadata, plan resharding, and bound cross-shard fan-out. Measure bytes, requests, and hot keys separately.

## Trade-offs and limits

Sharding adds routing, migration, and operational complexity. Optimize and scale a simpler database first when it meets requirements.

</details>

## Failure exercise

Simulate a tenant with half the traffic and assess shard imbalance.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Choose a shard key for orders and list the queries that become cross-shard. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 054](../../designs/06-distributed-systems/054-quorums-and-replica-overlap.md) · [Next: 056](../../designs/06-distributed-systems/056-consistent-hashing-and-rebalancing.md)
