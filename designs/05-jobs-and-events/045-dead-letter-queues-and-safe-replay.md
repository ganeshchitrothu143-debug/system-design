# 045 · Dead Letter Queues and Safe Replay

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

One malformed message retries forever and blocks useful processing.

## Prerequisites

Before this session, review: [041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md),[043](../../designs/05-jobs-and-events/043-retries-backoff-and-jitter.md)–[044](../../designs/05-jobs-and-events/044-idempotency-keys-and-duplicate-requests.md); retry limits, poison messages.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Should replaying a message skip the same validation that rejected it?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

After a bounded failure policy, quarantine the message with a safe diagnostic reason, attempts, timestamps, and original event identity. Alert on actionable growth. Fix the root cause, validate the replay scope, and replay at a controlled rate through the normal idempotent processing path. Preserve ordering constraints when a failed event precedes later events for the same entity.

## Trade-offs and limits

A dead-letter queue prevents endless retries but is not successful handling. Retained payloads may contain sensitive data and need access controls and expiry.

</details>

## Failure exercise

Replay a corrected batch twice and confirm no duplicate business effects.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write a replay runbook including selection, dry run, rate limit, monitoring, and stop conditions. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 044](../../designs/05-jobs-and-events/044-idempotency-keys-and-duplicate-requests.md) · [Next: 046](../../designs/05-jobs-and-events/046-reliable-webhook-delivery.md)
