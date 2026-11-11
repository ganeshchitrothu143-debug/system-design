# 073 · Service Identity and Least Privilege

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Any service on the internal network can modify payment records.

## Prerequisites

Before this session, review: [007](../../designs/01-http-and-apis/007-authentication-and-session-design.md),[026](../../designs/03-architecture-and-capacity/026-service-boundaries-and-microservice-extraction.md),[071](../../designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md); credentials, roles, network trust.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does a private network prove the caller is authorized?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Assign distinct service identities and grant only required operations on required resources. Authenticate service-to-service requests and validate audience or intended recipient when using tokens. Separate human, runtime, and deployment privileges. Prefer short-lived credentials where the platform supports them and record auditable access. Network controls complement identity rather than replace it.

## Trade-offs and limits

Fine-grained policies reduce blast radius but require maintenance and testing. Broad shared credentials are easy initially but make attribution and revocation difficult.

</details>

## Failure exercise

Use a notification-service identity to attempt a ledger write; it must be rejected.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | List the minimal permissions for API, worker, migration, and backup identities. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 072](../../designs/08-security-and-multi-tenancy/072-multi-tenant-data-isolation.md) · [Next: 074](../../designs/08-security-and-multi-tenancy/074-secrets-and-key-rotation.md)
