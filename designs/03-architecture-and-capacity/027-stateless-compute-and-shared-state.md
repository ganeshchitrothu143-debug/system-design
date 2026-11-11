# 027 · Stateless Compute and Shared State

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Requests succeed on one application instance but fail on another because sessions live only in memory.

## Prerequisites

Before this session, review: [007](../../designs/01-http-and-apis/007-authentication-and-session-design.md),[025](../../designs/03-architecture-and-capacity/025-modular-monolith-design.md); process memory, durable storage.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which state must survive an instance restart?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Keep durable user and workflow state outside individual application processes. Store sessions in an appropriate shared store or use a carefully validated token approach. Local caches may accelerate reads but must be disposable. A request should be routable to any healthy instance unless an explicit affinity requirement exists. Long-lived connections still need reconnect and state-recovery behavior.

## Trade-offs and limits

External state adds network calls and another dependency. Sticky sessions can reduce movement but do not preserve state when an instance fails.

</details>

## Failure exercise

Restart one instance and route the same user's next request elsewhere.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Classify session data, upload progress, cached catalog entries, and order records as durable or disposable. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 026](../../designs/03-architecture-and-capacity/026-service-boundaries-and-microservice-extraction.md) · [Next: 028](../../designs/03-architecture-and-capacity/028-api-gateways-and-backend-for-frontend.md)
