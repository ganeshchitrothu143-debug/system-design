# 030 · Architecture Decisions and Evolution

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A team cannot remember why it introduced a queue, so every review repeats the debate.

## Prerequisites

Before this session, review: [021](../../designs/03-architecture-and-capacity/021-requirements-and-quality-attributes.md)–[029](../../designs/03-architecture-and-capacity/029-protocols-for-real-time-communication.md); assumptions, alternatives, constraints.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

What evidence would justify reversing a decision?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Write a short architecture decision record: context, constraints, considered options, selected choice, consequences, and revisit conditions. Include measured or explicitly assumed scale. Record rejected alternatives fairly. Link decisions to diagrams and operational evidence. A later decision can supersede an earlier one without pretending the original context never existed.

## Trade-offs and limits

Documentation costs time, but a concise decision record avoids repeatedly reconstructing reasoning. Avoid giant documents that nobody updates.

</details>

## Failure exercise

Change a major assumption such as traffic, budget, or team size and identify which decision should be revisited.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write an ADR choosing a modular monolith for a new booking application. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 029](../../designs/03-architecture-and-capacity/029-protocols-for-real-time-communication.md) · [Next: 031](../../designs/04-performance-and-scaling/031-load-balancing-and-health-checks.md)
