# 065 · Feature Flags and Safe Rollback

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A feature is disabled, but new data written by it still breaks the old code.

## Prerequisites

Before this session, review: [017](../../designs/02-data-and-storage/017-schema-migrations-without-downtime.md),[064](../../designs/07-reliability-and-operations/064-rolling-canary-and-blue-green-deployments.md); configuration, compatibility.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does turning off a flag reverse its data changes?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use flags to separate deployment from feature exposure. Define safe defaults, evaluation scope, ownership, expiry, and cleanup. Test both states and consider deterministic assignment for experiments. A kill switch should be accessible during dependency failures. Reversible exposure does not imply reversible data; plan compatibility and repair for new records and side effects.

## Trade-offs and limits

Flags reduce release risk but add branching complexity and stale configuration. Too many interacting flags produce combinations that are hard to test.

</details>

## Failure exercise

Disable a feature after it has written data and test the fallback path against those records.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design a flag lifecycle with owner, rollout stages, emergency behavior, and removal date. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 064](../../designs/07-reliability-and-operations/064-rolling-canary-and-blue-green-deployments.md) · [Next: 066](../../designs/07-reliability-and-operations/066-circuit-breakers-and-bulkheads.md)
