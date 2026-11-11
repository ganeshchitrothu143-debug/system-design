# 022 · Traffic and Storage Estimation

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A service is sized using daily traffic divided by 24, then fails during a promotion.

## Prerequisites

Before this session, review: [021](../../designs/03-architecture-and-capacity/021-requirements-and-quality-attributes.md); arithmetic, bytes, seconds, averages.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Why is average traffic insufficient for capacity planning?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

For an illustrative workload of 8.64 million requests daily, average arrival rate is 100 per second. A ten-times peak means 1,000 per second. At 2 KB per response, payload egress is roughly 2 MB per second at peak before protocol overhead. For storage, multiply records by bytes and retention, then add indexes, replicas, backups, and growth headroom. State units and uncertainty rather than presenting guesses as facts.

## Trade-offs and limits

Estimates narrow choices; measurements validate them. Peak shape, hot keys, write amplification, and concurrent users matter more than a single large daily number.

</details>

## Failure exercise

Recalculate with larger payloads and a single hot customer. Determine which resource fails first.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Estimate requests, bandwidth, and one-year storage for 100,000 users creating ten 1 KB records daily. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 021](../../designs/03-architecture-and-capacity/021-requirements-and-quality-attributes.md) · [Next: 023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md)
