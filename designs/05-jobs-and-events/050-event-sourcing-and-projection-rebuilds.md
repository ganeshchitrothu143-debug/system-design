# 050 · Event Sourcing and Projection Rebuilds

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

An account needs a history of how its state changed, not just its current balance.

## Prerequisites

Before this session, review: [020](../../designs/02-data-and-storage/020-read-models-and-materialized-views.md),[047](../../designs/05-jobs-and-events/047-transactional-outbox.md)–[049](../../designs/05-jobs-and-events/049-sagas-and-compensating-actions.md); immutable records, versions.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Is an ordinary audit log automatically the authoritative event store?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

In event sourcing, accepted domain events are the source of truth and state is derived by applying them in order. Enforce expected stream versions when appending concurrent changes. Evolve event schemas carefully and rebuild projections into a separate target before switching readers. Snapshots speed recovery but do not replace the authoritative history unless the design explicitly allows it.

## Trade-offs and limits

Event sourcing supports historical reconstruction but increases complexity around schema evolution, deletion requirements, and projections. An ordinary CRUD model plus audit trail may be sufficient.

</details>

## Failure exercise

Rebuild a projection twice from the same event sequence and compare results.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Model a small account stream, including correction events rather than editing history. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 049](../../designs/05-jobs-and-events/049-sagas-and-compensating-actions.md) · [Next: 051](../../designs/06-distributed-systems/051-replication-and-failover.md)
