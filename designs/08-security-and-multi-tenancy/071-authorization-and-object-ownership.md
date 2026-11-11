# 071 · Authorization and Object Ownership

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A user changes an order ID in a URL and reads another customer's order.

## Prerequisites

Before this session, review: [007](../../designs/01-http-and-apis/007-authentication-and-session-design.md),[011](../../designs/02-data-and-storage/011-relational-data-modeling.md); authenticated identity, permissions, relationships.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Why is being logged in insufficient?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Authorize the action on the specific object using trusted identity and current policy. Scope database lookups to the permitted owner or tenant when appropriate. Deny by default and centralize policy mechanisms without skipping checks in workers, exports, or internal routes. Treat user-provided owner and role fields as untrusted. Decide whether forbidden object existence should be disclosed.

## Trade-offs and limits

Caching permissions improves speed but may delay revocation. Complex role systems can become harder to reason about than explicit relationships and actions.

</details>

## Failure exercise

Test access to another user's ID through direct reads, list filters, exports, and mutations.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Build an authorization matrix for owner, teammate, administrator, and unauthenticated caller. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 070](../../designs/07-reliability-and-operations/070-operational-readiness-and-runbooks.md) · [Next: 072](../../designs/08-security-and-multi-tenancy/072-multi-tenant-data-isolation.md)
