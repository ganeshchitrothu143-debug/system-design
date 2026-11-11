# 033 · Cache Invalidation and Staleness

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A writer deletes the cache entry, but an older in-flight reader repopulates stale data afterward.

## Prerequisites

Before this session, review: [032](../../designs/04-performance-and-scaling/032-cache-aside-design.md); concurrent readers and writers, versions.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Why can invalidate-after-write still race with readers?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

State an acceptable staleness window. Use TTLs to bound ordinary staleness, and consider versioned keys, conditional population, or source-version checks for stronger guarantees. Trace the read-miss, database-read, write-commit, invalidation, and cache-fill order explicitly. Critical decisions such as spending funds should use authoritative transactional checks rather than an eventually fresh display cache.

## Trade-offs and limits

Short TTLs increase database work. Stronger coherence adds coordination and may defeat the cache's simplicity. Different fields can have different freshness requirements.

</details>

## Failure exercise

Pause a cache-miss reader before population, commit a newer write, invalidate, then resume the reader.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Draw the stale-repopulation race and choose a mitigation for a price display versus payment authorization. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 032](../../designs/04-performance-and-scaling/032-cache-aside-design.md) · [Next: 034](../../designs/04-performance-and-scaling/034-cache-stampedes-hot-keys-and-eviction.md)
