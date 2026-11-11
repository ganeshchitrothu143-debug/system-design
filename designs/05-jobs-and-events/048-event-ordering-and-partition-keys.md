# 048 · Event Ordering and Partition Keys

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

An address-change event is processed after a newer one and restores an old address.

## Prerequisites

Before this session, review: [041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md),[047](../../designs/05-jobs-and-events/047-transactional-outbox.md); entity versions, partitions.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which events need ordering relative to each other?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Partition by the entity whose sequence matters and assign a monotonically increasing entity version at the source. Consumers track applied versions, reject stale updates, and define gap handling. Broker ordering may apply only within a partition and may be weakened by parallel processing or retries. Avoid assuming timestamps from different machines define a reliable global order.

## Trade-offs and limits

One ordered stream per hot entity limits parallelism. Global ordering is expensive and usually unnecessary when independent entities can progress separately.

</details>

## Failure exercise

Deliver versions 3, 2, and 3 again; then omit version 4 before delivering 5.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design a projection policy for stale, duplicate, and missing entity versions. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 047](../../designs/05-jobs-and-events/047-transactional-outbox.md) · [Next: 049](../../designs/05-jobs-and-events/049-sagas-and-compensating-actions.md)
