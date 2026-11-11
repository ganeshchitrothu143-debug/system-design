# 006 · Filtering Sorting and Search Contracts

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Users request arbitrary combinations of filters and sorts, producing slow and unpredictable queries.

## Prerequisites

Before this session, review: [002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md),[005](../../designs/01-http-and-apis/005-pagination-and-stable-ordering.md); predicates, indexes, pagination.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Should every database column be publicly filterable?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Expose an allowlist of filter fields and sort directions. Define case sensitivity, timezone interpretation, missing values, and maximum date ranges. Bind query values rather than concatenating SQL. Associate the cursor with the chosen filters so it cannot silently switch queries. Review expected access paths before adding an expensive filter. Free-text search has different matching and ranking rules from exact filtering; document those separately.

## Trade-offs and limits

Flexible search is convenient but creates more query shapes to index and test. Start from frequent user tasks and measure expensive combinations before expanding.

</details>

## Failure exercise

Submit an unknown sort key, malicious-looking value, empty date range, and cursor from another filter.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design a ticket-list contract supporting status, assignee, date range, and two approved sort orders. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 005](../../designs/01-http-and-apis/005-pagination-and-stable-ordering.md) · [Next: 007](../../designs/01-http-and-apis/007-authentication-and-session-design.md)
