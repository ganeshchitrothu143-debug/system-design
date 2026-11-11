# 068 · Graceful Degradation and Dependency Budgets

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A recommendation widget outage makes checkout unavailable.

## Prerequisites

Before this session, review: [021](../../designs/03-architecture-and-capacity/021-requirements-and-quality-attributes.md),[039](../../designs/04-performance-and-scaling/039-backpressure-and-load-shedding.md),[042](../../designs/05-jobs-and-events/042-timeouts-deadlines-and-cancellation.md),[066](../../designs/07-reliability-and-operations/066-circuit-breakers-and-bulkheads.md); critical versus optional work.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which features can disappear without violating the main user promise?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Classify dependencies by whether they are essential to correctness, necessary for the main function, or optional. Allocate time and concurrency budgets accordingly. Use bounded cached or omitted data only when it remains safe, and label degraded behavior when users need to know. Never fake successful payment or authorization merely to return a friendly response.

## Trade-offs and limits

Degradation improves usefulness during faults but adds alternate paths to test. A fallback that hits the same overloaded database may worsen the incident.

</details>

## Failure exercise

Disable each optional dependency and verify the core action still works within budget.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Define degraded behavior for product images, recommendations, stock validation, and payment authorization. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 067](../../designs/07-reliability-and-operations/067-backups-restore-and-disaster-recovery.md) · [Next: 069](../../designs/07-reliability-and-operations/069-failure-injection-and-resilience-testing.md)
