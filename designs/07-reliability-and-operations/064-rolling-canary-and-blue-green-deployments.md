# 064 · Rolling Canary and Blue Green Deployments

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A release works in tests but fails only for some production requests.

## Prerequisites

Before this session, review: [008](../../designs/01-http-and-apis/008-api-versioning-and-compatibility.md),[017](../../designs/02-data-and-storage/017-schema-migrations-without-downtime.md),[031](../../designs/04-performance-and-scaling/031-load-balancing-and-health-checks.md),[061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md); release compatibility, traffic routing.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

How can exposure be limited while gathering useful evidence?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

A rolling deployment replaces instances gradually; a canary exposes a controlled portion of traffic; blue-green keeps separate old and new environments for switching. In all cases, verify schema and protocol compatibility, readiness, draining, and rollback. Compare user outcomes and latency by version. Stop or roll back when predefined criteria fail, not only when CPU rises.

## Trade-offs and limits

Parallel environments cost capacity. A small canary may miss rare users or data shapes, and rolling releases run mixed versions. Database changes can make binary rollback unsafe.

</details>

## Failure exercise

Introduce a version-specific error and verify rollout stops before broad exposure.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Choose a release strategy and rollback conditions for an API with a compatible schema addition. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 063](../../designs/07-reliability-and-operations/063-actionable-alerting-and-incident-response.md) · [Next: 065](../../designs/07-reliability-and-operations/065-feature-flags-and-safe-rollback.md)
