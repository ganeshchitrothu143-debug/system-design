# 035 · Content Delivery Networks

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Users far from the origin load images slowly and origin bandwidth grows.

## Prerequisites

Before this session, review: [024](../../designs/03-architecture-and-capacity/024-tracing-a-request-through-the-network.md),[032](../../designs/04-performance-and-scaling/032-cache-aside-design.md)–[033](../../designs/04-performance-and-scaling/033-cache-invalidation-and-staleness.md); HTTP caching, geographic latency.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which responses can safely be shared among users?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Cache public immutable assets near users using content-versioned URLs and deliberate cache headers. Keep private or personalized responses out of shared caches unless keys and authorization semantics are explicitly safe. Define origin access controls and invalidation strategy. Measure cache hit ratio, origin fetch latency, and regional behavior. Signed access may restrict downloads but needs correct expiry and cache interaction.

## Trade-offs and limits

A CDN lowers latency and origin traffic but adds invalidation and configuration complexity. Caching a personalized response under a public key can expose data.

</details>

## Failure exercise

Request the same asset from multiple locations and test a private response for accidental shared caching.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design asset versioning for a web release so old HTML still loads compatible JavaScript. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 034](../../designs/04-performance-and-scaling/034-cache-stampedes-hot-keys-and-eviction.md) · [Next: 036](../../designs/04-performance-and-scaling/036-rate-limiting-and-quotas.md)
