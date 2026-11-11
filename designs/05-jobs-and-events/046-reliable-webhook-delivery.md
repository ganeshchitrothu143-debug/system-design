# 046 · Reliable Webhook Delivery

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A partner endpoint is down for an hour, then receives events out of order.

## Prerequisites

Before this session, review: [041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md)–[045](../../designs/05-jobs-and-events/045-dead-letter-queues-and-safe-replay.md); HTTPS, signatures, event IDs.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What does an HTTP success from the receiver actually acknowledge?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Persist outbound events and delivery attempts, then deliver asynchronously with deadlines and bounded retries. Sign the exact payload using a documented scheme that includes freshness protection; rotate secrets safely. Provide stable event IDs so receivers can deduplicate. Document whether acknowledgment means durable acceptance or completed processing. Do not promise ordering unless the delivery design enforces it.

## Trade-offs and limits

Webhooks reduce polling but require receiver security and recovery. A partner's success response cannot prove downstream business processing succeeded.

</details>

## Failure exercise

Return failures, delay responses, and repeat an event. Test deduplication and replay protection.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Specify a webhook contract with event ID, version, signature, retry policy, and status inspection. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 045](../../designs/05-jobs-and-events/045-dead-letter-queues-and-safe-replay.md) · [Next: 047](../../designs/05-jobs-and-events/047-transactional-outbox.md)
