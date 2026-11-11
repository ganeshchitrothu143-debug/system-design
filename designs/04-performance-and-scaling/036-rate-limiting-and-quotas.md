# 036 · Rate Limiting and Quotas

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

One client sends bursts that crowd out other users.

## Prerequisites

Before this session, review: [022](../../designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md),[027](../../designs/03-architecture-and-capacity/027-stateless-compute-and-shared-state.md); counters, time windows, atomic updates.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Should a short burst be permitted if average usage is reasonable?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

A token bucket refills at a fixed rate up to a capacity; each admitted request consumes tokens. Perform updates atomically at the chosen enforcement scope. Select keys such as tenant and operation, not only IP addresses shared by many users. Return a clear rejection and retry guidance where appropriate. Distinguish rate limits from concurrent-work limits and long-term quotas.

## Trade-offs and limits

Local limits are fast but approximate across instances. Central enforcement is more consistent but adds a dependency; define fail-open or fail-closed behavior per operation.

</details>

## Failure exercise

Send simultaneous requests through multiple instances and verify total admitted work stays within the documented approximation.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design a burst-tolerant limit for reads and a stricter limit for expensive exports. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 035](../../designs/04-performance-and-scaling/035-content-delivery-networks.md) · [Next: 037](../../designs/04-performance-and-scaling/037-autoscaling-and-capacity-headroom.md)
