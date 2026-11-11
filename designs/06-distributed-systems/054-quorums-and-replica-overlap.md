# 054 · Quorums and Replica Overlap

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A team assumes R plus W greater than N automatically means every read returns the latest write.

## Prerequisites

Before this session, review: [051](../../designs/06-distributed-systems/051-replication-and-failover.md)–[053](../../designs/06-distributed-systems/053-network-partitions-and-cap-tradeoffs.md); replica sets, versions, acknowledgments.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What additional rules are needed besides overlapping sets?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

With a fixed replica set, read and write quorum sizes can guarantee overlap when R + W exceeds N. But correctness also depends on version ordering, concurrent writes, replica membership, failure handling, and the protocol. Sloppy quorums and asynchronous repair change assumptions. Consensus protocols use quorum intersection together with leader and log rules; arithmetic alone is not a proof of linearizability.

## Trade-offs and limits

Larger quorums trade availability and latency for stronger coordination opportunities. Small clusters still need explicit failure and recovery protocols.

</details>

## Failure exercise

For N=3, enumerate read and write sets for R=2 and W=2, then introduce concurrent versions.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Explain what quorum overlap proves and what it does not prove. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 053](../../designs/06-distributed-systems/053-network-partitions-and-cap-tradeoffs.md) · [Next: 055](../../designs/06-distributed-systems/055-sharding-and-partition-key-selection.md)
