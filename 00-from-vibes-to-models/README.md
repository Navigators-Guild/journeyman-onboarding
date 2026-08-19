# Phase 0: From Vibes to Models

**Status:** curriculum outline

**Boundary introduced:** claim → repository evidence → explicit model → bounded change

## Purpose

Replace “the agent says it works” with a repeatable way to establish what the system is, what should change, and what evidence could reveal a mistake. This phase supplies the reasoning loop used by every later phase.

## Phase Outcome

Direct an agent to investigate a repository, separate facts from assumptions, express desired behavior as a falsifiable contract, make one bounded change, and produce an evidence packet another person can inspect.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **0.1 The Repository Is Evidence** | Plans must begin with the system that exists, not the system imagined in the prompt. | Inspect relevant files, manifests, commands, tests, Git state, and local instructions. Report facts with paths, assumptions, unknowns, and untouched areas before proposing edits. | A repository map whose key claims can be checked directly against files and command output. |
| **0.2 Behavior Before Implementation** | A request is ready when observable success, failure, constraints, and non-goals are clear enough to disagree about. | Rewrite the request as acceptance examples and boundary cases. Ask only questions whose answers would materially change the design. | A behavior contract with at least one happy path, rejection path, edge case, and explicit non-goal. |
| **0.3 Models, Invariants, and Failure Paths** | Reliable direction names the parts, state, boundaries, events, and rules that must remain true. | Model the relevant state and interactions before choosing an implementation. Identify hidden assumptions and rank failure paths by impact and likelihood. | A compact system model, invariant list, and failure table connected to planned checks. |
| **0.4 Changes as Falsifiable Hypotheses** | “This change solves the problem” is a hypothesis, not a conclusion. | Propose the smallest change that could satisfy the contract. For each important claim, name a check that could prove it false; then implement, inspect, and reconcile results. | A reviewed diff, targeted and broader check results, limitations, and a clear accept/revise/revert decision. |

## Practice Sequence

1. Give the learner a plausible but inaccurate description of the shared practice system.
2. Have the learner direct the agent to map the repository and correct the description with citations to local evidence.
3. Present an ambiguous behavior request and require an acceptance contract before edits.
4. Make one deliberately small change whose happy path can pass while an edge case fails.
5. Require the learner to find the unsupported claim, strengthen the check, and record what changed in their model.

## Shared-System Milestone

Create the first **reliability dossier** for the intentionally brittle application:

- repository and runtime map;
- intended users and critical behavior;
- known invariants and trust boundaries;
- risk-ranked weakness register;
- baseline commands and observed results;
- one bounded repair with a before/after evidence chain.

The dossier is revised throughout the course. It is not generated once and forgotten.

## Transfer to the Learner's Project

Repeat the repository map and behavior contract on a project the learner cares about. The implementation change may be tiny; the transfer goal is to discover where the learner's prior mental model disagrees with repository evidence.

## Phase Gate

The learner passes when they can present an evidence packet showing that they:

- distinguished repository facts, assumptions, preferences, and unknowns;
- wrote acceptance criteria before authorizing implementation;
- modeled at least one invariant and one failure path;
- limited the change to the stated objective;
- used a check capable of failing the implementation;
- identified what the evidence still does not establish.

Prompt fluency, code volume, and a polished demo do not satisfy this gate by themselves.

## Research Notes

This phase applies the current finding that AI-assisted completion and learning are different outcomes, while avoiding a ban on agents. It adds prediction, explanation, and reflection around authentic repository work. See findings 1–4 in [RESEARCH.md](../RESEARCH.md#findings-that-shape-the-course).

---

[Course overview](../README.md) · **Phase 0** · [Phase 1: How Programs Hold Together](../01-how-programs-hold-together/README.md)
