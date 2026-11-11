# 028 · API Gateways and Backend for Frontend

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A mobile screen makes twelve backend calls and downloads fields it never displays.

## Prerequisites

Before this session, review: [002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md),[026](../../designs/03-architecture-and-capacity/026-service-boundaries-and-microservice-extraction.md); routing, authentication, aggregation.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which orchestration belongs near the client and which business rules must stay in services?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

A gateway can route requests and enforce shared edge policies. A backend for frontend can aggregate screen-specific data and reshape it for mobile or web clients. Preserve authorization within owning services and propagate identity safely. Bound fan-out and deadlines, define partial responses, and avoid hiding long chains behind one endpoint. Keep core pricing or inventory rules out of duplicated presentation layers.

## Trade-offs and limits

Aggregation reduces client round trips but can become a bottleneck or tightly coupled orchestration service. Separate client-specific needs only when their differences justify the extra component.

</details>

## Failure exercise

Make one optional dependency slow and verify the page can return a documented partial response.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design a dashboard response with mandatory account data and optional recommendations from ordinary business rules. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 027](../../designs/03-architecture-and-capacity/027-stateless-compute-and-shared-state.md) · [Next: 029](../../designs/03-architecture-and-capacity/029-protocols-for-real-time-communication.md)
