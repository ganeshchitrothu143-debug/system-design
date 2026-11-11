# 038 · Connection Pools and Resource Budgets

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Twenty instances each open fifty database connections and exhaust a server limited to five hundred.

## Prerequisites

Before this session, review: [023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md),[027](../../designs/03-architecture-and-capacity/027-stateless-compute-and-shared-state.md),[037](../../designs/04-performance-and-scaling/037-autoscaling-and-capacity-headroom.md); connections, queues, timeouts.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Who owns the global connection budget?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Budget total connections across application instances, workers, migrations, and administration. Bound each pool and its wait queue, set acquisition timeouts, and monitor busy, idle, and waiting counts. Reuse connections safely and avoid holding one during unrelated network work. Include the maximum autoscaled instance count in the calculation, not only today's deployment.

## Trade-offs and limits

Larger pools can improve parallelism until database contention dominates. Too-small pools cause waiting; too-large pools move the queue into a more expensive resource.

</details>

## Failure exercise

Scale to the maximum instance count and run slow queries. Check total connections and acquisition latency.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Allocate a 500-connection limit across API, workers, and operational reserve. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 037](../../designs/04-performance-and-scaling/037-autoscaling-and-capacity-headroom.md) · [Next: 039](../../designs/04-performance-and-scaling/039-backpressure-and-load-shedding.md)
