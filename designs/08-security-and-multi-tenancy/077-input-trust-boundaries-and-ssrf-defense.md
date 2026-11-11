# 077 · Input Trust Boundaries and SSRF Defense

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A URL-preview service is asked to fetch an internal metadata endpoint.

## Prerequisites

Before this session, review: [003](../../designs/01-http-and-apis/003-request-validation-and-boundary-design.md),[024](../../designs/03-architecture-and-capacity/024-tracing-a-request-through-the-network.md),[071](../../designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md); URLs, DNS, server-side requests.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Why is a valid HTTPS URL not necessarily a safe destination?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Treat caller-supplied destinations as untrusted. Restrict schemes, hosts, ports, redirects, and outbound network access according to the business need. Resolve and validate addresses carefully, accounting for DNS rebinding and alternate address forms; enforce restrictions at the actual connection path. Prefer allowlisted destinations when feasible. Bound response size, duration, and decompression. Protect internal services even if application validation fails.

## Trade-offs and limits

Arbitrary URL fetching is inherently harder to secure than a constrained integration. Application checks and egress controls should reinforce each other.

</details>

## Failure exercise

Test redirects to private addresses, unexpected ports, huge responses, and DNS changes.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Draw trust boundaries for a URL-preview worker and define allowed outbound destinations. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 076](../../designs/08-security-and-multi-tenancy/076-audit-trails-and-tamper-evidence.md) · [Next: 078](../../designs/08-security-and-multi-tenancy/078-abuse-prevention-and-resource-isolation.md)
