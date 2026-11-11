# 049 · Sagas and Compensating Actions

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

An order reserves stock but payment fails after shipping preparation begins.

## Prerequisites

Before this session, review: [026](../../designs/03-architecture-and-capacity/026-service-boundaries-and-microservice-extraction.md),[041](../../designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md),[044](../../designs/05-jobs-and-events/044-idempotency-keys-and-duplicate-requests.md); state machines, partial failures.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Can every completed external action be literally rolled back?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Represent the workflow as explicit durable steps and outcomes. Use orchestration or choreography with stable operation IDs, retries, deadlines, and compensating actions where meaningful. Releasing stock may reverse a reservation; refunding payment is a new business action with its own failure modes. Keep uncertain states visible and provide reconciliation or human handling when automation cannot decide safely.

## Trade-offs and limits

Sagas allow workflows across transaction boundaries but expose intermediate states. They do not provide the same isolation as one database transaction.

</details>

## Failure exercise

Fail each step before and after its effect, including compensation itself.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design reserve, pay, and confirm states with compensation and unresolved-outcome paths. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 048](../../designs/05-jobs-and-events/048-event-ordering-and-partition-keys.md) · [Next: 050](../../designs/05-jobs-and-events/050-event-sourcing-and-projection-rebuilds.md)
