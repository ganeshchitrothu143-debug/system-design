# 005 · Pagination and Stable Ordering

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A list uses page numbers. New records arrive between requests, so users see duplicates.

## Prerequisites

Before this session, review: [002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md); sorting, unique IDs, comparison operators.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What happens to OFFSET 20 when five records are inserted at the beginning?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use a stable order such as created_at descending then id descending. Return an opaque cursor containing the last pair and the query context. The next query uses a matching comparison and an index that supports the filter and order. Cap page size and validate cursors. Keyset pagination reduces shifting caused by inserts before the cursor, but does not freeze records whose sort fields change. Use snapshot semantics if a complete consistent export is required.

## Concrete example

Illustrative SQL; adapt parameters and verify database behavior before use.

```sql
-- Descending keyset page; bind all parameters.
SELECT id, created_at, title
FROM tasks
WHERE owner_id = :owner_id
  AND (created_at, id) < (:last_time, :last_id)
ORDER BY created_at DESC, id DESC
LIMIT :bounded_page_size;
```

## Trade-offs and limits

Offsets are simple and support jumping to page numbers. Cursors scale better for sequential browsing but make arbitrary page jumps harder. A unique tie-breaker is essential.

</details>

## Failure exercise

Insert records sharing a timestamp between page requests. Check duplicates, omissions, and cursor behavior after deletion.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Simulate three pages of ten records with insertions and compare offset versus cursor results. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 004](../../designs/01-http-and-apis/004-consistent-api-error-responses.md) · [Next: 006](../../designs/01-http-and-apis/006-filtering-sorting-and-search-contracts.md)
