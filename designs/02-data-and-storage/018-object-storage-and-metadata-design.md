# 018 · Object Storage and Metadata Design

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Uploading large videos through the application server exhausts its connections.

## Prerequisites

Before this session, review: [007](../../designs/01-http-and-apis/007-authentication-and-session-design.md),[011](../../designs/02-data-and-storage/011-relational-data-modeling.md); files, ownership, checksums.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

How can direct upload avoid making an incomplete file publicly visible?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Store bytes in object storage and searchable metadata in a database. Authorize an upload session and issue a short-lived upload capability restricted to the intended object and operation. Track pending versus ready state; validate completion, size, checksum, and required scanning before publishing. The storage object and metadata transaction are separate, so reconciliation must detect orphaned uploads and missing objects.

## Trade-offs and limits

Direct upload reduces application bandwidth but complicates validation and cleanup. Object names are not authorization; download access still needs policy enforcement.

</details>

## Failure exercise

Interrupt an upload, forge a completion callback, and retry completion twice. Only a validated complete object becomes ready.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Design upload-session, finalize, download, and abandoned-upload cleanup flows. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 017](../../designs/02-data-and-storage/017-schema-migrations-without-downtime.md) · [Next: 019](../../designs/02-data-and-storage/019-data-retention-archival-and-deletion.md)
