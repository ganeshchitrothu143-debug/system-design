# 075 · Encryption and Data Protection Boundaries

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A system claims encryption protects data even from an application with full decryption access.

## Prerequisites

Before this session, review: [018](../../designs/02-data-and-storage/018-object-storage-and-metadata-design.md),[073](../../designs/08-security-and-multi-tenancy/073-service-identity-and-least-privilege.md)–[074](../../designs/08-security-and-multi-tenancy/074-secrets-and-key-rotation.md); transport, storage, keys.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Which attacker or exposure does each encryption layer address?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use transport encryption for data in transit and suitable storage encryption for persisted data. Identify who can decrypt, where keys live, and which services see plaintext. Application-level or field-level encryption can narrow access but complicates search, indexing, rotation, and recovery. Protect key availability and audit use. Encryption does not replace authorization or minimize retained data.

## Trade-offs and limits

Stronger separation can reduce exposure but adds operational burden. If the application is compromised while authorized to decrypt, storage encryption alone does not stop plaintext access.

</details>

## Failure exercise

Review a data flow and mark every point where plaintext exists.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Compare disk encryption and application-level field encryption for sensitive customer attributes. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 074](../../designs/08-security-and-multi-tenancy/074-secrets-and-key-rotation.md) · [Next: 076](../../designs/08-security-and-multi-tenancy/076-audit-trails-and-tamper-evidence.md)
