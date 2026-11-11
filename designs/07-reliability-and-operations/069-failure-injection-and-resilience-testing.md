# 069 · Failure Injection and Resilience Testing

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

The failover procedure looks correct on paper but has never run.

## Prerequisites

Before this session, review: [042](../../designs/05-jobs-and-events/042-timeouts-deadlines-and-cancellation.md),[061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md)–[068](../../designs/07-reliability-and-operations/068-graceful-degradation-and-dependency-budgets.md); hypotheses, bounded experiments.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What exact safety property should hold during the experiment?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Start with a hypothesis, scope, expected impact, observability, and stop conditions. Inject one controlled failure in a safe environment: latency, process crash, network loss, or dependency rejection. Observe user outcomes and durable state, then compare recovery with the stated invariant. Expand carefully only after smaller tests succeed. Capture surprising behavior as follow-up work.

## Trade-offs and limits

Realistic experiments expose hidden assumptions but can harm users if poorly bounded. Chaos is not a substitute for a precise question and recovery plan.

</details>

## Failure exercise

Kill one worker after committing its effect and before acknowledging the job.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write a test that proves duplicate delivery does not create duplicate orders, including evidence and cleanup. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 068](../../designs/07-reliability-and-operations/068-graceful-degradation-and-dependency-budgets.md) · [Next: 070](../../designs/07-reliability-and-operations/070-operational-readiness-and-runbooks.md)
