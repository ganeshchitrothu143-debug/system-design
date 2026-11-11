# 063 · Actionable Alerting and Incident Response

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

On-call engineers receive hundreds of CPU alerts but miss a broken checkout path.

## Prerequisites

Before this session, review: [061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md)–[062](../../designs/07-reliability-and-operations/062-service-level-indicators-and-error-budgets.md); severity, ownership, runbooks.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Would this alert tell someone to take an immediate useful action?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Page on user-impacting symptoms or imminent serious loss, then use diagnostic signals to investigate. Include owner, severity, affected function, evidence links, and a concise first-response procedure. Use deduplication, inhibition, and appropriate persistence to reduce noise. During incidents, establish coordination, record a timeline, mitigate impact, and communicate known facts separately from hypotheses.

## Trade-offs and limits

Sensitive alerts detect problems sooner but create fatigue. A threshold without an action or owner is often better as a dashboard signal.

</details>

## Failure exercise

Trigger an alert in a drill and ask an unfamiliar engineer to follow its instructions.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write an alert for growing checkout failures and a five-step initial response. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 062](../../designs/07-reliability-and-operations/062-service-level-indicators-and-error-budgets.md) · [Next: 064](../../designs/07-reliability-and-operations/064-rolling-canary-and-blue-green-deployments.md)
