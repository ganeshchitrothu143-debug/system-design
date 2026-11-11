# 061 · Logs Metrics and Distributed Traces

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A user reports a slow checkout, but each team sees only its own service logs.

## Prerequisites

Before this session, review: [023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md),[026](../../designs/03-architecture-and-capacity/026-service-boundaries-and-microservice-extraction.md); request IDs, measurements, service calls.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which evidence connects one request across boundaries?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use structured logs for discrete diagnostic events, metrics for aggregate behavior, and traces for request paths and timing. Propagate correlation context across services and queues while preserving trust boundaries. Record outcome, latency, and relevant safe identifiers. Avoid secrets and uncontrolled high-cardinality metric labels such as user IDs. Sampling and retention should preserve useful failure evidence within budget.

## Trade-offs and limits

More telemetry costs storage and can leak data. A trace explains a sampled execution, while metrics reveal population behavior; neither replaces the other.

</details>

## Failure exercise

Introduce a downstream delay and follow its effect from client latency to a specific span and safe log entry.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Specify telemetry for checkout without recording payment credentials or full personal payloads. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 060](../../designs/06-distributed-systems/060-cross-region-data-and-conflict-resolution.md) · [Next: 062](../../designs/07-reliability-and-operations/062-service-level-indicators-and-error-budgets.md)
