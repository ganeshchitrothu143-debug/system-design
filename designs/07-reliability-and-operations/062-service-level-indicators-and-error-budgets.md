# 062 · Service Level Indicators and Error Budgets

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A service reports 99.9 percent uptime even though many checkout requests fail.

## Prerequisites

Before this session, review: [021](../../designs/03-architecture-and-capacity/021-requirements-and-quality-attributes.md),[023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md),[061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md); ratios, measurement windows.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What user outcome should count as successful service?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Define an SLI such as the fraction of eligible checkout requests completed correctly within a latency threshold. Set an SLO over a clear window and document exclusions. The error budget is the allowed fraction of bad events; for one million eligible requests at 99.9 percent success, it is 1,000 bad requests. Time-based and request-based objectives are different. Use burn rate to detect rapid consumption.

## Concrete example

Illustrative pseudocode or contract, not a complete implementation.

```text
eligible_requests = 1_000_000
success_target = 0.999
allowed_bad_requests = eligible_requests * (1 - success_target)
                     = 1_000 requests
# This is a request-based budget, not minutes of downtime.
```

## Trade-offs and limits

Stricter targets cost engineering and infrastructure effort. Select targets from user needs and dependency constraints, not impressive round numbers.

</details>

## Failure exercise

Inject failures during both low and peak traffic and compare request-based and time-based measurements.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Define one availability and one latency SLI with numerator, denominator, window, and exclusions. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md) · [Next: 063](../../designs/07-reliability-and-operations/063-actionable-alerting-and-incident-response.md)
