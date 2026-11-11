# 029 · Protocols for Real Time Communication

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

A status page polls every second even when nothing changes, while chat needs messages in both directions.

## Prerequisites

Before this session, review: [001](../../designs/01-http-and-apis/001-http-api-request-response.md),[023](../../designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md)–[024](../../designs/03-architecture-and-capacity/024-tracing-a-request-through-the-network.md); connections, events, reconnects.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

Does the use case require bidirectional communication?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Use polling for simple infrequent updates, server-sent events for one-way server updates, and WebSockets when sustained bidirectional communication is needed. Regardless of transport, define authentication, heartbeats, reconnect backoff, message IDs, resumption, and slow-consumer handling. A live connection is not durable storage; fetch missed events from an authoritative source after reconnect.

## Trade-offs and limits

Persistent connections reduce repeated setup but consume resources and complicate load balancing. Transport selection does not by itself guarantee ordering or delivery.

</details>

## Failure exercise

Disconnect for thirty seconds, publish updates, then reconnect. Verify missed updates are recovered without duplicate effects.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Compare transports for an export-status page and a multiplayer collaboration interface. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 028](../../designs/03-architecture-and-capacity/028-api-gateways-and-backend-for-frontend.md) · [Next: 030](../../designs/03-architecture-and-capacity/030-architecture-decisions-and-evolution.md)
