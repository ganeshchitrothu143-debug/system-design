# 042 · Timeouts Deadlines and Cancellation

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A request with a one-second budget waits one second on each of three dependencies.

## Prerequisites

Before this session, review: [023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md)–[024](../../designs/03-architecture-and-capacity/024-tracing-a-request-through-the-network.md),[041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md); elapsed time, network failures.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Should every downstream call receive the full original timeout?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Set an end-to-end deadline and pass the remaining budget to downstream work. Distinguish connection setup, response headers, body transfer, and overall operation timeouts. Stop optional work when the budget is exhausted. Cancellation is cooperative and may arrive after a remote write commits; a client timeout means the outcome is unknown, not necessarily failed. Resolve uncertain writes using operation IDs and status queries.

## Trade-offs and limits

Very short timeouts create unnecessary failures; long ones hold resources. Choose budgets from latency distributions and user requirements rather than arbitrary identical values.

</details>

## Failure exercise

Delay a response after its write commits. Ensure the caller does not assume no effect occurred.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Allocate a 1,000 ms deadline across gateway, service, database, and response overhead. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md) · [Next: 043](../../designs/05-jobs-and-events/043-retries-backoff-and-jitter.md)
