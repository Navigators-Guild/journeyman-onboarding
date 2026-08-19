# Phase 4: How Systems Communicate and Fail

**Status:** curriculum outline

**Boundary introduced:** local operation → concurrent or remote interaction → partial result

## Purpose

Make time, ordering, duplication, delay, overload, and partial failure visible. Learners stop treating an API call as a local function call and start directing communication as a protocol with bounded behavior.

## Phase Outcome

Direct an agent to define an API contract, design safe timeout and retry behavior, protect shared state under concurrency, manage queued work and overload, and explain the consistency guarantees of a multi-component workflow.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **4.1 APIs Are Protocol Contracts** | A communicating pair shares syntax, semantics, sequencing, errors, and compatibility expectations. | Inventory clients and servers, define valid requests and responses, error meanings, authentication context, version behavior, size limits, and observability fields. | Consumer and provider contract checks, negative cases, and a compatibility example. |
| **4.2 Timeouts, Retries, and Idempotency** | No response does not mean no effect; a retry can duplicate work or amplify an outage. | Set deadlines from the user budget, classify retryable failures, cap attempts, add backoff and jitter, and design a stable idempotency identity for consequential operations. | Lost-response and duplicate-request tests plus evidence that total retry time stays within budget. |
| **4.3 Concurrency, Ordering, and Ownership** | Concurrent work is safe only when ownership, allowed orderings, and conflict behavior preserve invariants. | Model interleavings around shared state. Compare serialization, locking, optimistic conflict detection, immutability, and partitioned ownership. | A deterministic race test or stress test that reproduces the prior hazard and verifies the chosen invariant. |
| **4.4 Queues, Delivery, and Backpressure** | A queue moves pressure and failure; it does not remove them. Delivery can be delayed, repeated, reordered, or abandoned. | Define producer/consumer rates, capacity, delivery semantics, deduplication, retry/dead-letter policy, poison-message handling, and overload response. | Duplicate, reorder, consumer-crash, poison-message, and saturation exercises with visible queue health. |
| **4.5 Partial Failure, Consistency, and Capacity** | A distributed workflow needs a declared acceptable outcome when only some participants succeed. | Trace a timeline across components, identify consistency requirements, choose compensation or reconciliation, estimate capacity, and define degradation before exhaustion. | Fault injection across each boundary, reconciliation evidence, and a measured or reasoned capacity limit. |

## Practice Sequence

1. Replace an undocumented shared-system call with a small explicit protocol contract.
2. Simulate a remote operation that succeeds while its response is lost.
3. Observe an unsafe retry, then add idempotency and a bounded retry budget.
4. Reproduce one shared-state race under controlled scheduling or repeated stress.
5. Saturate a queue or worker pool and verify the intended backpressure and degraded behavior.
6. Draw the final event timeline and reconcile every possible partial result.

## Shared-System Milestone

Harden one cross-boundary workflow with:

- a versioned API or message contract;
- deadline, retry, and idempotency decisions;
- an explicit concurrency owner;
- queue capacity and failure policy where relevant;
- fault-injection results and a reconciliation procedure;
- an observable capacity or degradation threshold.

## Transfer to the Learner's Project

Choose one external call, background job, or concurrent operation. Ask what happens if it is slow, duplicated, reordered, completed without acknowledgment, or attempted during overload. Test one answer rather than accepting the agent's description.

## Phase Gate

The learner passes when they can:

- distinguish a timeout from a confirmed failure;
- justify whether an operation may be retried;
- state an idempotency identity and its retention boundary;
- name allowed concurrent orderings and the owner of shared state;
- explain queue delivery and overload behavior without saying “exactly once” casually;
- show how a partial result becomes visible and is reconciled.

## Research Notes

This phase joins a durable event-ordering model with current production guidance for retries and idempotency. The recipes are context-dependent; the transferable skill is reasoning about time and partial knowledge. See finding 7 in [RESEARCH.md](../RESEARCH.md#7-networks-turn-ordinary-operations-into-time--and-duplication-sensitive-protocols).

---

[Phase 3](../03-how-data-survives/README.md) · **Phase 4** · [Phase 5: How Changes Stay Safe](../05-how-changes-stay-safe/README.md)
