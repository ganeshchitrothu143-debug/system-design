# 074 · Secrets and Key Rotation

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

An API key is committed to source control and remains valid after being removed from the latest file.

## Prerequisites

Before this session, review: [007](../../designs/01-http-and-apis/007-authentication-and-session-design.md),[073](../../designs/08-security-and-multi-tenancy/073-service-identity-and-least-privilege.md); credentials, deployment configuration.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does deleting the visible string revoke the secret?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Store secrets in an appropriate secret-management system and inject them at runtime under least privilege. Avoid logs, browser bundles, and build artifacts. On exposure, revoke or rotate the credential and investigate use; history cleanup alone is insufficient. Plan overlap for old and new keys during rotation, update consumers, verify adoption, then retire the old key.

## Trade-offs and limits

Rotation improves recovery but can cause outages if consumers cache keys indefinitely. Separate credential rotation from encryption-key data migration, which may require keeping old decryption capability.

</details>

## Failure exercise

Rotate a credential while old and new application instances coexist.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Write a rotation sequence with verification and rollback that never prints the key. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 073](../../designs/08-security-and-multi-tenancy/073-service-identity-and-least-privilege.md) · [Next: 075](../../designs/08-security-and-multi-tenancy/075-encryption-and-data-protection-boundaries.md)
