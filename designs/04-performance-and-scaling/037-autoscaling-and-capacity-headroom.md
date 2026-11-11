# 037 · Autoscaling and Capacity Headroom

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Instances scale up only after queues grow beyond the user deadline.

## Prerequisites

Before this session, review: [022](../../designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md)–[023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md),[031](../../designs/04-performance-and-scaling/031-load-balancing-and-health-checks.md); startup delay, bottlenecks.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What happens while new capacity is still starting?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Choose signals tied to work: queue age, concurrency, CPU, or request demand. Estimate startup and warm-up time, keep headroom, and use cooldowns to avoid oscillation. Cap scale based on downstream capacity and budget. Scale-in must drain active work. Scheduled demand can justify pre-scaling, but unexpected bursts still need admission control.

## Trade-offs and limits

More application instances cannot repair a saturated shared database. Aggressive scaling can multiply connections and make an outage worse.

</details>

## Failure exercise

Inject a burst shorter than instance startup time and observe rejected work and queue age.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Define scale-up, scale-down, and maximum-instance rules for a worker fleet. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 036](../../designs/04-performance-and-scaling/036-rate-limiting-and-quotas.md) · [Next: 038](../../designs/04-performance-and-scaling/038-connection-pools-and-resource-budgets.md)
