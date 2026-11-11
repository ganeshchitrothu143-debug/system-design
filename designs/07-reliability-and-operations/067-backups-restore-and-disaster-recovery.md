# 067 · Backups Restore and Disaster Recovery

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A replicated database faithfully copies an accidental deletion to every replica.

## Prerequisites

Before this session, review: [019](../../designs/02-data-and-storage/019-data-retention-archival-and-deletion.md),[051](../../designs/06-distributed-systems/051-replication-and-failover.md); durable storage, replication, recovery objectives.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Can replication recover the state before the mistake?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Define recovery point objective as tolerated data loss and recovery time objective as tolerated restoration time. Maintain protected backups and logs suited to the desired restore point. Test restoration, integrity checks, key availability, configuration, and application startup in an isolated environment. Document how deleted personal data is handled after restore. Keep backup credentials and deletion permissions separated where practical.

## Trade-offs and limits

More frequent and geographically separate backups cost money and complexity. A successful backup job is not evidence of a successful restore.

</details>

## Failure exercise

Restore a selected point in time and measure actual data loss and recovery duration.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write a recovery plan for loss of the primary database and separately for accidental logical deletion. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 066](../../designs/07-reliability-and-operations/066-circuit-breakers-and-bulkheads.md) · [Next: 068](../../designs/07-reliability-and-operations/068-graceful-degradation-and-dependency-budgets.md)
