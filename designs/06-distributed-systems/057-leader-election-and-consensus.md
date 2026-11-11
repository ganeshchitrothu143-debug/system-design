# 057 · Leader Election and Consensus

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Two nodes each believe they are leader and issue conflicting commands.

## Prerequisites

Before this session, review: [051](../../designs/06-distributed-systems/051-replication-and-failover.md)–[054](../../designs/06-distributed-systems/054-quorums-and-replica-overlap.md); majority, logs, terms.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Why is choosing a leader insufficient unless old leaders are constrained?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Consensus protocols such as Raft coordinate a replicated log using terms, elections, and quorum-based commitment. A leader must follow protocol rules; merely holding an old leadership belief does not authorize committing new entries. Use a mature implementation instead of inventing election logic. Distinguish safety, which prevents conflicting committed history, from liveness, which depends on timing and reachable majorities.

## Trade-offs and limits

Consensus provides a strong coordination foundation but adds latency and can stop progress without a quorum. It does not atomically include arbitrary external side effects.

</details>

## Failure exercise

Partition an old leader away from the majority and observe which side may commit.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Explain a three-node majority and why two isolated single nodes cannot each commit safely. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 056](../../designs/06-distributed-systems/056-consistent-hashing-and-rebalancing.md) · [Next: 058](../../designs/06-distributed-systems/058-distributed-locks-leases-and-fencing.md)
