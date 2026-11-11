# 034 · Cache Stampedes Hot Keys and Eviction

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A popular item expires and ten thousand requests all query the database.

## Prerequisites

Before this session, review: [032](../../designs/04-performance-and-scaling/032-cache-aside-design.md)–[033](../../designs/04-performance-and-scaling/033-cache-invalidation-and-staleness.md); expiration, memory limits, concurrency.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Would increasing cache size alone prevent synchronized misses?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Coalesce concurrent loads for the same key, add expiration jitter, and optionally serve bounded stale data while one refresh runs. Limit refresh work and timeouts. Identify hot keys separately from total cache volume; one key can overwhelm a shard. Choose eviction policy and object-size limits based on workload, and measure hit rate alongside backend load.

## Trade-offs and limits

Serving stale data improves availability only when the business tolerates it. A refresh lock needs expiry and recovery; failure must not block the key forever.

</details>

## Failure exercise

Expire a hot key under concurrent load and kill the refresh owner.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Specify stampede protection and maximum acceptable stale age for a public catalog page. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 033](../../designs/04-performance-and-scaling/033-cache-invalidation-and-staleness.md) · [Next: 035](../../designs/04-performance-and-scaling/035-content-delivery-networks.md)
