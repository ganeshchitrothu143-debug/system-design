# 019 · Data Retention Archival and Deletion

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

An activity table grows forever while old exports remain accessible after users delete accounts.

## Prerequisites

Before this session, review: [011](../../designs/02-data-and-storage/011-relational-data-modeling.md),[018](../../designs/02-data-and-storage/018-object-storage-and-metadata-design.md); timestamps, dependencies.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does deleting one database row remove every copy of the data?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Classify data by purpose and define retention periods, ownership, and dependencies. Use bounded deletion or archival jobs with checkpoints. Include object storage, search indexes, caches, analytics, and backup policies in the data map. Preserve a deletion marker where needed to prevent delayed events from resurrecting removed records. Backup expiry and restoration procedures must account for prior deletions.

## Trade-offs and limits

Archival supports history and recovery but adds storage and access-control obligations. Retaining everything indefinitely makes deletion and incident response harder.

</details>

## Failure exercise

Restore an older backup in a test environment and check how previously recorded deletions are reapplied.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Map all copies of a user-uploaded file and define what delete means for each. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 018](../../designs/02-data-and-storage/018-object-storage-and-metadata-design.md) · [Next: 020](../../designs/02-data-and-storage/020-read-models-and-materialized-views.md)
