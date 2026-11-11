# 070 · Operational Readiness and Runbooks

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A service launches without anyone knowing how to restore it or stop runaway work.

## Prerequisites

Before this session, review: [061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md)–[069](../../designs/07-reliability-and-operations/069-failure-injection-and-resilience-testing.md); ownership, deployment, recovery.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Who can safely operate the system at two in the morning?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Before launch, identify owners, dashboards, alerts, SLOs, dependencies, capacity limits, backup and restore evidence, release rollback, access controls, and incident procedures. A runbook should state symptoms, checks, safe actions, expected results, and escalation. Practice it with someone other than its author. Include how to stop changes or replay safely.

## Trade-offs and limits

Readiness should scale to the service's risk. A checklist is useful only when backed by working mechanisms and evidence.

</details>

## Failure exercise

Ask a teammate to diagnose a simulated queue backlog using only the runbook.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Create a one-page readiness review for a small background export service. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 069](../../designs/07-reliability-and-operations/069-failure-injection-and-resilience-testing.md) · [Next: 071](../../designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md)
