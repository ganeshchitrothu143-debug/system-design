# 043 · Retries Backoff and Jitter

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Five service layers each retry three times and overload a failing dependency.

## Prerequisites

Before this session, review: [042](../../designs/05-jobs-and-events/042-timeouts-deadlines-and-cancellation.md); transient versus permanent failure, idempotence.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

How many attempts can one user request trigger across layers?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Retry only recoverable failures when the operation is safe or protected by idempotency. Centralize ownership of retries, cap attempts and total elapsed time, and use exponential backoff with jitter. Respect explicit retry guidance when applicable. Apply a retry budget so recovery traffic cannot dominate normal traffic. Never retry invalid input unchanged.

## Trade-offs and limits

Retries can hide brief faults but amplify overload and duplicate effects. Independent retries at multiple layers multiply attempts; three attempts at each of five layers can create up to 243 leaf attempts.

</details>

## Failure exercise

Simulate a dependency outage and count total attempts per user operation.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Define retry rules for a GET, a validation error, and a payment submission with an idempotency key. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 042](../../designs/05-jobs-and-events/042-timeouts-deadlines-and-cancellation.md) · [Next: 044](../../designs/05-jobs-and-events/044-idempotency-keys-and-duplicate-requests.md)
