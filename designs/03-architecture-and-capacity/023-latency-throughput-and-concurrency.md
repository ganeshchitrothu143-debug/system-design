# 023 · Latency Throughput and Concurrency

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A service handles 100 requests per second, but many users wait several seconds.

## Prerequisites

Before this session, review: [022](../../designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md); percentiles, averages, time units.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Can adequate average throughput coexist with unacceptable tail latency?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Latency is elapsed time per operation, throughput is completed work per unit time, and concurrency is work in progress. In a stable system, Little's Law relates average concurrency to average arrival rate times average time in system. At 100 requests per second and 0.2 seconds average latency, about 20 requests are in flight on average. Inspect p50, p95, and p99 separately; averages hide slow tails. Include queue waiting in end-to-end latency.

## Trade-offs and limits

Increasing concurrency may improve utilization until a bottleneck saturates, after which queues and tail latency grow. Little's Law is not a justification for unbounded concurrency.

</details>

## Failure exercise

Slow a downstream dependency and observe queue length, in-flight work, and p99 latency.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Calculate concurrency for three latency levels and propose a bounded admission policy. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 022](../../designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md) · [Next: 024](../../designs/03-architecture-and-capacity/024-tracing-a-request-through-the-network.md)
