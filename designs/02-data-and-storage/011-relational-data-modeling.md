# 011 · Relational Data Modeling

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Orders store customer names and products in comma-separated text. Reporting and updates become unreliable.

## Prerequisites

Before this session, review: [002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md); records, IDs, one-to-many relationships.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which facts describe an order at purchase time and which describe the current customer?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use separate customer, order, product, and order-line tables with primary and foreign keys. Store quantity and purchase-time unit price on the order line so catalog changes do not rewrite historical totals. Add constraints for required values and valid quantities. Choose deletion behavior explicitly. A relational model describes both relationships and invariants; application validation alone cannot protect against every writer.

## Trade-offs and limits

Normalization reduces accidental duplication, while selected snapshots preserve history and reduce joins. Copying an address for an order is intentional historical data, not automatically a modeling mistake.

</details>

## Failure exercise

Delete or rename a product after purchase and confirm the original receipt still makes sense.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Sketch tables and constraints for orders with multiple line items and shipping addresses. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 010](../../designs/01-http-and-apis/010-synchronous-and-asynchronous-api-contracts.md) · [Next: 012](../../designs/02-data-and-storage/012-sql-versus-document-and-key-value-storage.md)
