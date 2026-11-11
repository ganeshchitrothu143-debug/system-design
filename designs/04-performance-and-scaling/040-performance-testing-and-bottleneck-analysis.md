# 040 · Performance Testing and Bottleneck Analysis

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A benchmark reports impressive throughput using tiny payloads and an empty database.

## Prerequisites

Before this session, review: [022](../../designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md)–[023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md),[031](../../designs/04-performance-and-scaling/031-load-balancing-and-health-checks.md)–[039](../../designs/04-performance-and-scaling/039-backpressure-and-load-shedding.md); measurement, representative data.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What assumption makes the benchmark unlike production?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use representative request mixes, data cardinality, payloads, and arrival patterns. Separate warm-up from steady state and include spikes and endurance runs. Measure client-observed latency, errors, resource saturation, and useful throughput together. An open arrival model exposes queue growth under overload; closed-loop clients can slow themselves and hide it. Change one suspected bottleneck at a time and compare evidence.

## Trade-offs and limits

Synthetic tests cannot reproduce every real workload. Production-like realism costs resources, but small isolated benchmarks should not be advertised as whole-system capacity.

</details>

## Failure exercise

Add a slow dependency and verify the load generator still reports intended arrival pressure and failures.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write a performance-test plan with pass criteria and a stop condition to protect the test environment. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 039](../../designs/04-performance-and-scaling/039-backpressure-and-load-shedding.md) · [Next: 041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md)
