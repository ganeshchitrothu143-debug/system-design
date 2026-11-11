# 002 · REST Resource and Endpoint Design

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A task app has separate createTask, finishTask, and loadTask URLs. Mobile clients cannot predict their behavior.

## Prerequisites

Before this session, review: [001](../../designs/01-http-and-apis/001-http-api-request-response.md); resource IDs, HTTP methods, JSON.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Should completing a task delete it?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Model tasks as resources: POST /tasks creates one, GET /tasks/42 reads it, and PATCH /tasks/42 changes allowed fields such as status. Keep identity stable across status changes. Check ownership before every operation and return a saved representation or a documented empty response. A cancellation that starts a business workflow can be a separate cancellation resource. REST does not forbid domain actions; choose a contract that exposes meaningful state.

## Trade-offs and limits

Resource-oriented APIs are predictable, but forcing every business operation into a generic field update can hide rules. Do not allow clients to patch price, owner, or audit fields merely because those fields exist.

</details>

## Failure exercise

Try completing a task owned by another user and completing an already completed task. Define both outcomes.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design five endpoints for tasks and comments, including missing IDs and invalid transitions. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 001](../../designs/01-http-and-apis/001-http-api-request-response.md) · [Next: 003](../../designs/01-http-and-apis/003-request-validation-and-boundary-design.md)
