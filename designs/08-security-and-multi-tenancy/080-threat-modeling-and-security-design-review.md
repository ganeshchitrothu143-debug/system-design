# 080 · Threat Modeling and Security Design Review

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A feature passes functional tests but allows an attacker to trigger privileged actions.

## Prerequisites

Before this session, review: [071](../../designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md)–[079](../../designs/08-security-and-multi-tenancy/079-privacy-deletion-and-data-minimization.md); data flows, trust boundaries, attacker goals.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Where can untrusted input influence a privileged decision?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Draw actors, data stores, flows, and trust boundaries. Identify assets and plausible attacker goals, then examine spoofing, tampering, disclosure, privilege escalation, and resource exhaustion along each path. Prioritize by impact and realistic exposure. Convert mitigations into concrete checks and tests, assign owners, and record residual risks. Revisit the model when architecture or permissions change.

## Trade-offs and limits

A threat model should guide engineering decisions rather than produce an enormous generic checklist. It complements testing and code review.

</details>

## Failure exercise

Choose one boundary and attempt to bypass identity, object ownership, or resource limits.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Review an export-and-download feature from upload authorization through final file access. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 079](../../designs/08-security-and-multi-tenancy/079-privacy-deletion-and-data-minimization.md) · [Next: 081](../../designs/09-product-designs/081-url-shortener.md)
