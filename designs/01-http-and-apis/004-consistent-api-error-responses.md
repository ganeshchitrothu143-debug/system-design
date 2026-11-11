# 004 · Consistent API Error Responses

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

The frontend parses English error messages to decide which field to highlight. A wording change breaks it.

## Prerequisites

Before this session, review: [001](../../designs/01-http-and-apis/001-http-api-request-response.md),[003](../../designs/01-http-and-apis/003-request-validation-and-boundary-design.md); status codes, validation, identifiers.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which error fields should be stable for programs and which can change for people?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Return a stable machine-readable error type or code, an appropriate HTTP status, a safe explanation, and optional field errors. A request ID lets support correlate logs without exposing stack traces. RFC 9457 offers a standard problem-details shape with type, title, status, detail, and instance. If using it, keep the HTTP status and body status consistent. For unexpected failures, give a generic message while recording diagnostics privately.

## Trade-offs and limits

Detailed errors help users fix input, but may reveal account existence or internal structure. Decide which distinctions an unauthorized caller is permitted to learn.

</details>

## Failure exercise

Change the human message without changing the code. Verify the UI still handles the error. Trigger an unexpected database failure and inspect exposed fields.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Specify errors for invalid input, missing authentication, insufficient permission, conflict, and temporary outage. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 003](../../designs/01-http-and-apis/003-request-validation-and-boundary-design.md) · [Next: 005](../../designs/01-http-and-apis/005-pagination-and-stable-ordering.md)
