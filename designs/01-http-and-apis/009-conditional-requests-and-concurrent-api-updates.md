# 009 · Conditional Requests and Concurrent API Updates

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Two editors load the same task. The last save overwrites the first editor's changes.

## Prerequisites

Before this session, review: [001](../../designs/01-http-and-apis/001-http-api-request-response.md)–[002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md); versions, concurrent reads and writes.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Where must the version check happen to prevent a race?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Return an ETag representing the resource version. Require If-Match on updates and compare it atomically with the stored version while applying the change. A stale precondition returns 412; the client reloads and offers a merge or retry. A read followed by an unprotected update is insufficient because another write can occur between them. Conditional GET with If-None-Match can return 304 when a cached representation remains valid.

## Trade-offs and limits

Optimistic concurrency works well when conflicts are uncommon. It exposes conflicts to clients; hot objects may need different workflows or finer-grained updates.

</details>

## Failure exercise

Have two clients update version 7 simultaneously. Exactly one should succeed against version 7.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write a timeline and an atomic update predicate for two edits to one task. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 008](../../designs/01-http-and-apis/008-api-versioning-and-compatibility.md) · [Next: 010](../../designs/01-http-and-apis/010-synchronous-and-asynchronous-api-contracts.md)
