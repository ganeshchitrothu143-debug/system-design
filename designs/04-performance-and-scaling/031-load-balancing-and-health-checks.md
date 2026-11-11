# 031 · Load Balancing and Health Checks

[Curriculum index](../../README.md) · [Track index](README.md)

## The problem

Traffic continues reaching an instance that is running but cannot serve requests.

## Prerequisites

Before this session, review: [024](../../designs/03-architecture-and-capacity/024-tracing-a-request-through-the-network.md),[027](../../designs/03-architecture-and-capacity/027-stateless-compute-and-shared-state.md); multiple instances, routing.

If an item is unfamiliar, use the [starter glossary](../../START-HERE.md#starter-glossary) and linked earlier notes. You should be able to explain those items in your own words before moving to the worked approach.

## Predict first

How does process liveness differ from readiness to receive traffic?

Write your answer and sketch the relevant state or request sequence before opening the solution.

<details>
<summary>Hint</summary>

Start with one normal operation, then pause it just before and just after its durable change. Identify who owns the truth and what another caller can observe. Use the question above to decide which assumption needs testing.

</details>

<details>
<summary>Worked approach — open after your attempt</summary>

## One workable approach

Distribute requests across eligible instances using a policy suited to request cost and connection behavior. Separate liveness from readiness: restarting a live process will not necessarily repair a shared dependency failure. Add thresholds and draining so transient health failures do not cause flapping and removed instances can finish work. Consider zone distribution and uneven long-lived connections.

## Trade-offs and limits

Aggressive checks detect faults quickly but can remove too much capacity during a shared outage. A health endpoint that checks every dependency may turn one dependency failure into total unavailability.

</details>

## Failure exercise

Drain an instance during active requests and simulate a shared database slowdown.

Record the initial state, action sequence, expected durable state, and observed result. Explain the root cause of any mismatch before changing the design.

## 40-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the prerequisites without looking at the notes. |
| 10 min | Read the problem, predict the outcome, and sketch your approach. |
| 15 min | Define health-check semantics and a safe removal sequence for an API instance. |
| 5 min | Run or trace the failure exercise and improve the design. |
| 5 min | Explain your decision, one alternative, and one limitation aloud. |

## Explain and revisit

- What invariant or user promise are you protecting?
- Why does your chosen approach fit this problem?
- What evidence would make you change the design?

Record your attempt in the [practice log](../../PRACTICE-LOG.md). Revisit after 2–3 days and again after a week: redraw the flow and explain the failure without rereading first.

---

[Previous: 030](../../designs/03-architecture-and-capacity/030-architecture-decisions-and-evolution.md) · [Next: 032](../../designs/04-performance-and-scaling/032-cache-aside-design.md)
