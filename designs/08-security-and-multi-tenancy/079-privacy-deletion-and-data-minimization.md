# 079 · Privacy Deletion and Data Minimization

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A user deletes an account, but copies remain in logs and analytics exports.

## Prerequisites

Before this session, review: [019](../../designs/02-data-and-storage/019-data-retention-archival-and-deletion.md),[072](../../designs/08-security-and-multi-tenancy/072-multi-tenant-data-isolation.md),[076](../../designs/08-security-and-multi-tenancy/076-audit-trails-and-tamper-evidence.md); data inventory, dependencies, retention.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which collected fields are actually needed for the product purpose?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Minimize collection and map each retained field to a purpose, owner, and retention policy. Propagate deletion through derived stores and downstream copies with auditable progress. Use tombstones or deletion records to prevent resurrection from delayed events and restores where required. Separate legitimately retained records and explain their handling. Obtain appropriate jurisdiction-specific guidance for legal obligations rather than assuming one universal rule.

## Trade-offs and limits

Deletion can conflict with immutable history and recovery needs. Plan those boundaries before data spreads; pseudonymization is not automatically anonymization.

</details>

## Failure exercise

Delete a test identity and search every mapped store, then replay an older event.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design a deletion workflow with retries, evidence, and explicit retained-data exceptions. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 078](../../designs/08-security-and-multi-tenancy/078-abuse-prevention-and-resource-isolation.md) · [Next: 080](../../designs/08-security-and-multi-tenancy/080-threat-modeling-and-security-design-review.md)
