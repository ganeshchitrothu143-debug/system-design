# 003 · Request Validation and Boundary Design

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

An API accepts negative quantities and enormous text bodies, causing corrupt orders and high memory use.

## Prerequisites

Before this session, review: [001](../../designs/01-http-and-apis/001-http-api-request-response.md)–[002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md); JSON types, required fields, string length.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Is frontend validation sufficient when requests can be sent directly?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Validate transport size before parsing, then check the schema, then domain rules. For an order line, require a known product ID and an integer quantity within a business limit. Reject unknown writable fields or explicitly ignore them according to the contract. Recheck stock and price against authoritative data inside the relevant write operation. Normalize only values whose meaning is preserved; passwords and identifiers may be case-sensitive.

## Trade-offs and limits

Strict validation catches mistakes early but can break clients if new optional fields are rejected. Separate the public input schema from the database model and plan compatibility.

</details>

## Failure exercise

Send quantity as a string, zero, a decimal, and an oversized number; bypass the UI entirely.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write an input/output table for eight invalid requests and explain which layer rejects each. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md) · [Next: 004](../../designs/01-http-and-apis/004-consistent-api-error-responses.md)
