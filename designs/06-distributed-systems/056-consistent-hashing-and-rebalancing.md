# 056 · Consistent Hashing and Rebalancing

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Adding one cache node remaps most keys under hash(key) modulo node_count.

## Prerequisites

Before this session, review: [055](../../designs/06-distributed-systems/055-sharding-and-partition-key-selection.md); hash functions, nodes, key ownership.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

How can membership changes move fewer keys?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Place nodes and keys on a hash ring or use another stable assignment scheme. Virtual nodes can spread ownership more evenly. On membership changes, transfer the affected ranges while handling reads and writes during movement. Keep assignment versions and monitor skew. Consistent hashing reduces expected movement; it does not solve one extremely hot key or guarantee equal load for unequal-sized objects.

## Trade-offs and limits

Stable assignment eases scaling but adds membership and migration complexity. Data stores need durable transfer semantics beyond cache remapping.

</details>

## Failure exercise

Add and remove nodes, measure moved keys, then test a highly popular single key.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Sketch ownership before and after adding a node and describe migration verification. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 055](../../designs/06-distributed-systems/055-sharding-and-partition-key-selection.md) · [Next: 057](../../designs/06-distributed-systems/057-leader-election-and-consensus.md)
