# Phase 2: How Codebases Hold Together

**Status:** curriculum outline

**Boundary introduced:** responsibility → interface → dependency → compatible change

## Purpose

Move from reasoning about one program path to reasoning about a codebase that must change over time. Learners direct structure according to ownership and change pressure, not file-count aesthetics or whatever pattern the agent names first.

## Phase Outcome

Direct an agent to map responsibilities and dependencies, improve a boundary without a rewrite, manage external dependencies and configuration, and preserve an intentionally defined compatibility contract.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **2.1 Responsibilities and Information Hiding** | A useful module hides a design decision likely to change and owns a coherent responsibility. | Identify reasons the code changes, decisions leaking across files, and concerns that move together. Propose boundaries around ownership rather than arbitrary size. | A responsibility map and a bounded extraction that reduces duplicated knowledge. |
| **2.2 Interfaces and Dependency Direction** | A boundary is valuable when callers depend on a stable contract rather than internal details. | Map callers and callees, data crossing the boundary, error semantics, and permitted dependency direction. Compare at least two interface shapes. | Contract tests plus a dependency check showing that the intended direction holds. |
| **2.3 Dependencies, Configuration, and Builds** | Every dependency and configuration value expands the system's behavior, trust, and reproducibility surface. | Inventory direct dependencies, versions, licenses, maintenance signals, runtime settings, defaults, and secret-handling. Remove, pin, isolate, or document according to risk. | A clean build from declared inputs, configuration validation, and a dependency decision record. |
| **2.4 Refactoring Without Wishful Rewrites** | Refactoring changes structure while preserving a defined behavior envelope. | Establish characterization evidence, make reversible structural steps, and keep feature work separate. Identify behavior that is intentionally preserved versus corrected. | Before/after checks, reviewed intermediate diffs, and no unexplained behavior change. |
| **2.5 Compatibility and Architecture Decisions** | A public contract includes behavior that downstream users reasonably rely on, not just a function signature. | Identify consumers, compatibility promises, migration needs, and rollback constraints. Record the consequential decision and rejected alternatives. | Consumer-facing compatibility checks, version decision, migration note, and concise decision record. |

## Practice Sequence

1. Ask the agent to map the shared system by responsibilities and change reasons.
2. Find a rule duplicated across two or more components.
3. Characterize current behavior, including one undesirable behavior that must temporarily remain compatible.
4. Move ownership behind a defined interface in reviewable steps.
5. Break the dependency rule deliberately, make the architecture check catch it, and restore the boundary.
6. Review one third-party dependency and one configuration path as parts of the architecture.

## Shared-System Milestone

Untangle one high-risk responsibility without rewriting the application. Deliver:

- current and intended responsibility maps;
- an interface contract and dependency direction;
- characterization and contract tests;
- a dependency/configuration inventory for the changed slice;
- an architecture decision explaining the trade-off and migration path.

## Transfer to the Learner's Project

Choose one place where a small change routinely touches unrelated files. Have the agent identify the knowledge being duplicated, then improve one boundary while preserving a named compatibility envelope.

## Phase Gate

The learner passes when they can:

- explain why a boundary exists and what decision it hides;
- identify both compile-time and runtime dependencies;
- compare interface alternatives according to real consumers;
- distinguish refactoring evidence from new-feature evidence;
- state a compatibility promise and demonstrate it;
- reject an unnecessary abstraction even when the agent proposes it confidently.

## Research Notes

The phase rests on information hiding as a durable architecture principle and current compatibility and API guidance as operational references. See finding 5 and the Phase 2 row in [RESEARCH.md](../RESEARCH.md#phase-to-evidence-map).

---

[Phase 1](../01-how-programs-hold-together/README.md) · **Phase 2** · [Phase 3: How Data Survives](../03-how-data-survives/README.md)
