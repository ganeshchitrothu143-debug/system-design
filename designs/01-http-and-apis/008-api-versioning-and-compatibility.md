# 008 · API Versioning and Compatibility

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A server renames a response field while an older mobile app is still installed.

## Prerequisites

Before this session, review: [002](../../designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md)–[004](../../designs/01-http-and-apis/004-consistent-api-error-responses.md); public contracts, optional fields.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Can deployment order alone upgrade clients that are offline?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Prefer compatible additions and preserve existing meanings. Adding an optional response field is often safe, but clients that reject unknown fields need attention. Changing units, required fields, enum values, or error semantics can also break clients. Use an explicit version boundary for incompatible contracts and run old and new versions during migration. Measure version usage and communicate a retirement policy. Contract tests should exercise representative older clients.

## Trade-offs and limits

Supporting versions costs maintenance. Frequent version bumps are not a substitute for careful contract design; never silently repurpose an existing field.

</details>

## Failure exercise

Run a saved old request against the new server and validate the old response assumptions.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Plan migration from price in whole currency units to price in minor units without silently multiplying charges. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 007](../../designs/01-http-and-apis/007-authentication-and-session-design.md) · [Next: 009](../../designs/01-http-and-apis/009-conditional-requests-and-concurrent-api-updates.md)
