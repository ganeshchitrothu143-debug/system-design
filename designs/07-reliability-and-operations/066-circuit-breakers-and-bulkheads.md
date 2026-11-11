# 066 · Circuit Breakers and Bulkheads

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A failing email provider consumes all request threads and prevents order reads.

## Prerequisites

Before this session, review: [038](../../designs/04-performance-and-scaling/038-connection-pools-and-resource-budgets.md)–[043](../../designs/05-jobs-and-events/043-retries-backoff-and-jitter.md); dependency failures, resource limits.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which resources should failures be prevented from sharing?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

A circuit breaker stops repeated calls after a defined failure policy, then probes recovery with limited traffic. A bulkhead reserves separate concurrency or resource budgets for different dependencies or workloads. Use both with timeouts and meaningful fallbacks. Avoid treating business rejections as infrastructure failures. Monitor breaker state and useful outcomes.

## Trade-offs and limits

Breakers can fail to recover if probes are poorly designed or can oscillate if thresholds are unstable. Bulkheads reserve capacity that may be idle but contain damage.

</details>

## Failure exercise

Make email calls hang and verify order reads retain their own resource budget.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Specify breaker transitions and separate concurrency pools for payment and notification calls. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 065](../../designs/07-reliability-and-operations/065-feature-flags-and-safe-rollback.md) · [Next: 067](../../designs/07-reliability-and-operations/067-backups-restore-and-disaster-recovery.md)
