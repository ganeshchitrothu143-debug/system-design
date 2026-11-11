# 041 · Durable Job Queues and Worker Acknowledgments

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A worker removes a job from a queue and crashes before completing it.

## Prerequisites

Before this session, review: [010](../../designs/01-http-and-apis/010-synchronous-and-asynchronous-api-contracts.md),[014](../../designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md); persisted state, worker crashes.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

When should a worker acknowledge a message?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use a durable queue with explicit delivery and acknowledgment semantics. A worker receives a job, performs recoverable work, durably records the outcome, then acknowledges. A visibility timeout or lease permits redelivery after failure. If the outcome commits but acknowledgment is lost, delivery can repeat; make effects idempotent. Monitor oldest-job age, attempt counts, and processing failures.

## Trade-offs and limits

At-least-once delivery trades possible duplicates for recovery. Queue durability settings and acknowledgment guarantees vary; a queue alone cannot guarantee exactly one external effect.

</details>

## Failure exercise

Crash before processing and again after the effect but before acknowledgment.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Draw both crash timelines and state how the next worker discovers whether work already happened. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 040](../../designs/04-performance-and-scaling/040-performance-testing-and-bottleneck-analysis.md) · [Next: 042](../../designs/05-jobs-and-events/042-timeouts-deadlines-and-cancellation.md)
