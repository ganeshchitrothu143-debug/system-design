# Start here

[Curriculum index](README.md)

## First session

Begin with [001: HTTP API Requests and Responses](designs/01-http-and-apis/001-http-api-request-response.md). Design the request and response for saving one task. Before reading the solution, predict the response for valid input, invalid input, and a missing task.

## Prerequisite policy

Each lesson names the prior notes and concepts needed for its exercise. Read a range such as 011–015 as the inclusive sequence. You do not need to master the whole curriculum before building anything. If you cannot explain a prerequisite, take a separate short session to practice it. For implementation exercises, basic variables, functions, conditions, collections, and running a small program in a language you know are useful. Paper designs do not require a cloud account.

## Session rhythm

| Minutes | Work |
| --- | --- |
| 5 | Recall a previous concept and check today's prerequisites. |
| 10 | Understand the concrete problem and predict a failure. |
| 15 | Design or implement one small behavior. |
| 5 | Debug a failure and revise the approach. |
| 5 | Explain why it works and what it does not guarantee. |

Use JavaScript or TypeScript for small simulations if familiar. SQL examples illustrate database operations; they need an appropriate local database, schema, and driver to run. Pseudocode is intentionally not an application. Do not copy a security or distributed-system sketch into production without implementation-specific review.

## Evidence of learning

A note is practiced when you can state its problem, draw the flow, explain a trade-off, and predict a failure. Reading alone is not completion. Keep unfinished questions visible in the [practice log](PRACTICE-LOG.md). Review after 2–3 days and one week. If family or work interrupts a session, leave a short next-action note and resume there.

## Starter glossary

| Term | Plain meaning |
| --- | --- |
| Client / server | A caller requesting work and a program handling it. |
| API contract | The agreed requests, responses, and observable behavior. |
| Resource / ID | A thing the system manages and its identifier. |
| JSON | A text representation of structured values. |
| Durable | Expected to survive specified failures under the storage system's guarantees. |
| State / transition | What is true now and a permitted change to it. |
| Invariant | A rule that must remain true, such as no negative stock. |
| Transaction | A group of database operations committed or rolled back together. |
| Concurrency | Multiple operations overlapping in time. |
| Atomic | Appearing as one indivisible operation at the stated boundary. |
| Idempotent effect | Repeating the same operation does not repeat its business effect. |
| Latency / throughput | Time per operation / amount of completed work per unit time. |
| Queue | Buffered work waiting for a consumer. |
| Replica / shard | A copy of data / a partition of data. |
| Cache | A reusable copy or computed result with an explicit freshness policy. |
| Consistency | The guarantees callers observe about data across operations. |
| Authentication / authorization | Establishing identity / deciding allowed actions. |
| Tenant | A customer or organization with an isolation boundary. |
| Recovery point / recovery time | Tolerated data loss / tolerated restoration time. |

## Design review checklist

State requirements and assumptions; identify the source of truth; trace one write and read; mark transaction boundaries; account for duplicates, delays, crashes, and unauthorized requests; measure outcomes; describe recovery. Add infrastructure only when a requirement justifies it.
