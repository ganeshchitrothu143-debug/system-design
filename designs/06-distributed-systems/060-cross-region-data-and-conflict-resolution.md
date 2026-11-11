# 060 · Cross Region Data and Conflict Resolution

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Two regions edit the same customer record while disconnected.

## Prerequisites

Before this session, review: [051](../../designs/06-distributed-systems/051-replication-and-failover.md)–[059](../../designs/06-distributed-systems/059-distributed-ids-and-clock-behavior.md); ownership, replication lag, conflict policies.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which conflicts can be merged and which require one authority?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Separate region-local data from globally coordinated invariants. Assign a home region or single writer for sensitive entities when that simplifies correctness. For multi-writer data, define merge semantics per field or operation and preserve enough history to reconcile. Last-write-wins based on wall clocks can discard valid changes and depends on clock assumptions. Make failover and failback procedures explicit.

## Trade-offs and limits

Active-active writes can improve local availability but make conflicts and invariants harder. Region routing may add latency yet simplify business correctness.

</details>

## Failure exercise

Edit different fields and then the same field during a partition; inspect convergence after recovery.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design regional ownership and failover for orders while allowing preferences to merge separately. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 059](../../designs/06-distributed-systems/059-distributed-ids-and-clock-behavior.md) · [Next: 061](../../designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md)
