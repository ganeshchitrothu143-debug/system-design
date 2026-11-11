# 059 · Distributed IDs and Clock Behavior

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A timestamp-based ID generator produces duplicates when the clock moves backward.

## Prerequisites

Before this session, review: [011](../../designs/02-data-and-storage/011-relational-data-modeling.md),[055](../../designs/06-distributed-systems/055-sharding-and-partition-key-selection.md); uniqueness, time, collisions.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does chronological-looking order imply reliable global event order?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Choose IDs based on uniqueness scope, generation independence, sort requirements, and exposure risks. Random IDs avoid central allocation but need sufficient entropy and collision handling. Sequence allocation is simple but may require coordination. Time-plus-worker schemes require unique worker identities and a documented policy for clock rollback and sequence exhaustion. Use explicit entity versions for causal ordering.

## Trade-offs and limits

Compact ordered IDs can improve storage locality but reveal information or depend on coordination. Random IDs may affect index locality. Neither design removes authorization checks.

</details>

## Failure exercise

Restart generators with duplicated worker IDs and simulate a backward clock adjustment.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Compare database sequences, random UUIDs, and time-based IDs for orders. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 058](../../designs/06-distributed-systems/058-distributed-locks-leases-and-fencing.md) · [Next: 060](../../designs/06-distributed-systems/060-cross-region-data-and-conflict-resolution.md)
