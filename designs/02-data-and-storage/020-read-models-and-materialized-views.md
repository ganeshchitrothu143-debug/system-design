# 020 · Read Models and Materialized Views

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A dashboard recomputes expensive aggregates for every request.

## Prerequisites

Before this session, review: [011](../../designs/02-data-and-storage/011-relational-data-modeling.md),[014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md); joins, derived data, freshness.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which data is authoritative when a dashboard total disagrees with orders?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Maintain a derived read model suited to the query while keeping an explicit source of truth. Refresh periodically or update from reliable changes. Record a source version or processing watermark so users and operators can understand freshness. Make replay idempotent and define how to rebuild without exposing partially populated results. Reconcile aggregates against source records.

## Trade-offs and limits

Precomputation makes reads faster but spends storage and introduces lag or additional write work. Avoid a projection if a simple indexed query already meets the need.

</details>

## Failure exercise

Replay the same update twice, miss one update, and rebuild the view. Verify detection and recovery.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design daily order totals with a five-minute freshness target and a safe rebuild process. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 019](../../designs/02-data-and-storage/019-data-retention-archival-and-deletion.md) · [Next: 021](../../designs/03-architecture-and-capacity/021-requirements-and-quality-attributes.md)
