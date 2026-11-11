# 039 · Backpressure and Load Shedding

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A service accepts work faster than it can finish and memory usage climbs continuously.

## Prerequisites

Before this session, review: [023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md),[036](../../designs/04-performance-and-scaling/036-rate-limiting-and-quotas.md),[038](../../designs/04-performance-and-scaling/038-connection-pools-and-resource-budgets.md); queues, deadlines, priority.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Is accepting every request more available if most later time out?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Bound queues and concurrent work. Propagate backpressure where producers can slow down, and reject excess work early where they cannot. Use deadlines and priorities so already-expired or optional work does not consume scarce capacity. Distinguish temporary overload from permanent invalid input. Observe queue age and useful completions, not only accepted requests.

## Trade-offs and limits

Early rejection is visible but can preserve successful service for admitted users. Priority schemes need fairness so one class is not starved indefinitely.

</details>

## Failure exercise

Double arrival rate while holding processing capacity fixed. Verify memory remains bounded and admitted requests meet their target.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design an overload policy with separate budgets for checkout and background analytics. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 038](../../designs/04-performance-and-scaling/038-connection-pools-and-resource-budgets.md) · [Next: 040](../../designs/04-performance-and-scaling/040-performance-testing-and-bottleneck-analysis.md)
