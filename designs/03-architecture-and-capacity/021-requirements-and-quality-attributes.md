# 021 · Requirements and Quality Attributes

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A request to build a fast booking system has no agreement on what success means.

## Prerequisites

Before this session, review: [001](../../designs/01-http-and-apis/001-http-api-request-response.md)–[020](../../designs/02-data-and-storage/020-read-models-and-materialized-views.md) as needed; business workflows, measurable outcomes.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Would users prefer a delayed confirmation or two people owning the same seat?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Separate functional behavior from quality attributes. State actors, supported operations, exclusions, scale assumptions, latency targets, availability, correctness, privacy, and budget. Identify invariants such as one confirmed owner per seat. Turn vague terms into measurable targets with an observation window and measurement point. Record unresolved assumptions and test the riskiest ones before choosing infrastructure.

## Trade-offs and limits

Requirements can conflict: stronger coordination may increase latency during failures. Resolve priorities with the business rather than hiding them inside technology choices.

</details>

## Failure exercise

Change peak traffic by ten times and introduce a regional outage. Identify which promises still hold.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write a one-page requirements brief for a small appointment booking system. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 020](../../designs/02-data-and-storage/020-read-models-and-materialized-views.md) · [Next: 022](../../designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md)
