# 072 · Multi Tenant Data Isolation

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A cached report from tenant A is returned to tenant B.

## Prerequisites

Before this session, review: [011](../../designs/02-data-and-storage/011-relational-data-modeling.md),[032](../../designs/04-performance-and-scaling/032-cache-aside-design.md),[071](../../designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md); tenant identity, shared resources.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Where does tenant context need to appear besides the database query?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Derive tenant context from authenticated, authorized membership. Carry it through queries, uniqueness constraints, cache keys, object paths, queue jobs, logs, and exports. Consider database row-level policies as defense in depth where supported, with carefully tested connection context. Shared tables, separate schemas, and separate databases provide different isolation and operational costs.

## Trade-offs and limits

Shared infrastructure is economical but increases the importance of comprehensive boundaries. Separate databases strengthen some isolation while multiplying migrations and operations.

</details>

## Failure exercise

Run identical object IDs for two tenants and exercise reads, caches, background jobs, and administrative paths.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Create a tenant-boundary checklist for a report export from request to download. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 071](../../designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md) · [Next: 073](../../designs/08-security-and-multi-tenancy/073-service-identity-and-least-privilege.md)
