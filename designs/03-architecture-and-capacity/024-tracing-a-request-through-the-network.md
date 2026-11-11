# 024 · Tracing a Request through the Network

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

The API code executes quickly, but a user's first request is slow.

## Prerequisites

Before this session, review: [001](../../designs/01-http-and-apis/001-http-api-request-response.md),[023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md); DNS, TCP, TLS, HTTP.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which delays occur before application code begins?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Trace name resolution, connection establishment, TLS negotiation, proxy routing, application processing, database work, and response transfer. Some requests reuse connections and skip parts of this path. Measure from the client and at service boundaries; a server timer alone misses network and browser delay. Distinguish DNS failure, connection refusal, TLS failure, timeout, and application errors. Set deadlines across the complete operation.

## Trade-offs and limits

Connection reuse saves setup time but needs lifecycle and capacity management. More proxies can provide useful controls while adding hops and failure points.

</details>

## Failure exercise

Compare cold and reused connections, then simulate DNS failure and a slow response body.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Draw the request path for a browser calling an API that reads a database. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md) · [Next: 025](../../designs/03-architecture-and-capacity/025-modular-monolith-design.md)
