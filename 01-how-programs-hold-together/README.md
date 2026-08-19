# Phase 1: How Programs Hold Together

**Status:** curriculum outline

**Boundary introduced:** input → state transition → output or explicit failure

## Purpose

Teach the machinery inside a program as a set of design choices the learner can model and direct. Syntax remains the agent's job; the learner must be able to say what state may exist, how it may change, and what failure means.

## Phase Outcome

Direct an agent to represent valid states clearly, isolate side effects, define contracts, handle expected failure deliberately, and select data structures according to behavior and scale.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **1.1 State, Control, and Time** | A program is a sequence of state observations and transitions; order and ownership determine behavior. | Trace one user action through inputs, branches, loops, state changes, and outputs. Identify state that is local, shared, derived, or externally owned. | A trace for success and failure, plus tests that distinguish important branch and ordering behavior. |
| **1.2 Types and Valid States** | A representation should make valid states easy to construct and invalid states hard to represent. | Inventory values that are absent, malformed, mutually exclusive, or conditionally valid. Propose representations and boundary validation with trade-offs. | Construction and boundary tests showing rejected invalid states and preserved invariants. |
| **1.3 Functions, Contracts, and Side Effects** | A component is easier to reason about when its inputs, outputs, obligations, and effects are explicit. | Separate calculation from I/O where useful. State preconditions, postconditions, side effects, and ownership rather than merely extracting arbitrary helper functions. | Contract-focused tests and a call/effect map that reveals where external state changes. |
| **1.4 Errors and Recovery** | Expected failure is part of the interface; programmer defects and recoverable conditions need different treatment. | Create an error taxonomy: who can act, what context they need, what may be retried, and what must stop. Preserve original causes without leaking secrets. | Tests for each consequential error path and user/operator messages appropriate to the audience. |
| **1.5 Data Structures and Cost** | A structure encodes operations and their costs; convenient behavior at ten items may fail at ten million. | List dominant reads, writes, ordering needs, uniqueness rules, expected size, and memory constraints before selecting a structure. Measure when the choice affects risk. | A choice record, representative-size test or benchmark, and a stated capacity boundary. |

## Practice Sequence

1. Trace a shared-system action that currently mixes input parsing, business rules, storage, and display.
2. Name its states and transitions without changing code.
3. Ask the agent to redesign the representation so one known invalid state cannot be constructed internally.
4. Isolate a calculation from its side effects and test it through its contract.
5. Introduce an expected failure and verify that it reaches the right audience with enough context.
6. Compare two data-structure choices using the actual dominant operation and a representative workload.

## Shared-System Milestone

Harden one critical workflow so that it has:

- an explicit state-transition model;
- enforced input and internal invariants;
- a visible boundary between calculation and effects;
- a documented error taxonomy;
- evidence that its dominant operation remains acceptable at the intended scale.

## Transfer to the Learner's Project

Choose one workflow with confusing conditionals or scattered validation. Direct the agent to trace it before refactoring, then improve one representation or contract without expanding the feature scope.

## Phase Gate

The learner passes when they can:

- explain a program path as state transitions rather than recite syntax;
- identify where an invariant is enforced and where untrusted input enters;
- distinguish a returned value from a side effect;
- decide which failures are recoverable, retryable, or defects;
- justify a data-structure choice using operations and expected scale;
- verify that the refactor preserved intended behavior while rejecting an invalid case.

## Research Notes

The design uses mature ideas about contracts, valid-state representation, and explicit error semantics. Language-specific sources are treated as examples of general principles, not required technologies. See finding 5 in [RESEARCH.md](../RESEARCH.md#5-reliable-software-comes-from-explicit-boundaries-and-enforced-invariants).

---

[Phase 0](../00-from-vibes-to-models/README.md) · **Phase 1** · [Phase 2: How Codebases Hold Together](../02-how-codebases-hold-together/README.md)
