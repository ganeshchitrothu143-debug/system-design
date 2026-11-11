# 017 · Schema Migrations without Downtime

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

New code expects a renamed column while old instances still run.

## Prerequisites

Before this session, review: [008](../../designs/01-http-and-apis/008-api-versioning-and-compatibility.md),[011](../../designs/02-data-and-storage/011-relational-data-modeling.md),[014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md); rolling deployments.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which schema can both application versions safely use?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use expand, migrate, contract. Add the new compatible structure first, deploy code that tolerates both, backfill in bounded resumable batches, verify consistency, then switch reads and writes deliberately. Remove the old structure only after old clients and rollback dependencies disappear. Watch database locks, replication lag, and backfill load. A migration is a multi-release workflow, not only one DDL command.

## Trade-offs and limits

Keeping both structures temporarily increases complexity. Immediate destructive changes are simpler only when downtime and rollback constraints allow them.

</details>

## Failure exercise

Stop the backfill halfway and restart it. Run old and new code together during the transition.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Plan splitting full_name into display_name and structured fields without guessing how every name should split. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 016](../../designs/02-data-and-storage/016-optimistic-and-pessimistic-concurrency.md) · [Next: 018](../../designs/02-data-and-storage/018-object-storage-and-metadata-design.md)
