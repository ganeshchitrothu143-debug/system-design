# 078 · Abuse Prevention and Resource Isolation

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

One tenant submits thousands of large exports and delays everyone else's work.

## Prerequisites

Before this session, review: [036](../../designs/04-performance-and-scaling/036-rate-limiting-and-quotas.md),[039](../../designs/04-performance-and-scaling/039-backpressure-and-load-shedding.md),[072](../../designs/08-security-and-multi-tenancy/072-multi-tenant-data-isolation.md); quotas, expensive operations.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does a request-per-second limit account for unequal request cost?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Budget expensive resources such as concurrent exports, bytes processed, retained storage, and worker time per tenant. Use fair scheduling, bounded input size, admission control, and separate pools when needed. Meter actual usage and handle cancellation and expiry. Rate limits alone do not stop a few extremely expensive requests.

## Trade-offs and limits

Isolation protects neighbors but can reduce peak utilization. Weighted fairness allows deliberate service tiers while requiring starvation safeguards.

</details>

## Failure exercise

Run one heavy tenant alongside many small tenants and measure each tenant's completion latency.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design quotas and queue scheduling for free and paid export users. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 077](../../designs/08-security-and-multi-tenancy/077-input-trust-boundaries-and-ssrf-defense.md) · [Next: 079](../../designs/08-security-and-multi-tenancy/079-privacy-deletion-and-data-minimization.md)
