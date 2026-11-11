# 026 · Service Boundaries and Microservice Extraction

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Inventory must scale and deploy independently, but extracting it breaks checkout transactions.

## Prerequisites

Before this session, review: [025](../../designs/03-architecture-and-capacity/025-modular-monolith-design.md); deployment, APIs, failure boundaries.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which new failures appear when a local function becomes a remote call?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Extract around business ownership and a concrete scaling or delivery need. Define a stable contract, move data ownership, and plan compatibility during migration. Remote calls need timeouts, authentication, observability, and partial-failure handling. Replace assumptions about shared transactions with reservations, explicit states, and reconciliation where necessary. Keep a rollback plan and measure whether the extraction solves its original problem.

## Trade-offs and limits

Independent deployment and scaling come with network latency, coordination cost, and more operational work. Small services are not automatically good boundaries.

</details>

## Failure exercise

Make inventory unreachable after an order is created. Determine the order state and recovery action.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write an extraction plan that avoids both services independently owning inventory truth. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 025](../../designs/03-architecture-and-capacity/025-modular-monolith-design.md) · [Next: 027](../../designs/03-architecture-and-capacity/027-stateless-compute-and-shared-state.md)
