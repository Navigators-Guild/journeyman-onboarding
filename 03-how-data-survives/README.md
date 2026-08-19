# Phase 3: How Data Survives

**Status:** curriculum outline

**Boundary introduced:** accepted fact → durable state → compatible evolution → recovery

## Purpose

Teach that persistence is a set of guarantees about truth, interruption, concurrency, and recovery—not a feature obtained merely by adding a database. Learners must decide which facts matter and where their rules are enforced.

## Phase Outcome

Direct an agent to define a source of truth, enforce data invariants, choose transaction and consistency behavior, evolve a schema safely, treat caches as derived state, and demonstrate restoration after failure.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **3.1 Source of Truth, Schema, and Constraints** | Durable rules belong close enough to the source of truth that every write path must obey them. | Inventory facts, identifiers, relationships, optional values, retention needs, and writers. Propose schema and constraints from invariants rather than current form fields. | Tests that attempt invalid writes through more than one path and show the store rejects them. |
| **3.2 Transactions, Atomicity, and Isolation** | A multi-step update needs a declared all-or-nothing boundary and a concurrency guarantee suited to its invariant. | Draw the transaction boundary, identify concurrent interleavings, select isolation or explicit coordination, and define retry behavior for aborted transactions. | Interruption and concurrency tests showing no committed partial state or invariant violation. |
| **3.3 Migrations and Compatible Evolution** | A schema change is a protocol between old data, old code, new code, and recovery tooling. | Propose expand–migrate–contract steps, preconditions, data validation, rollout order, rollback limits, and backup needs. Avoid irreversible steps until compatibility is demonstrated. | Migration on a production-shaped copy, old/new compatibility checks, counts or checksums, and a rehearsed fallback. |
| **3.4 Caches and Derived State** | A cache is a disposable view only when the source of truth and invalidation rules are explicit. | Name the authoritative data, freshness tolerance, keying, eviction, invalidation events, and behavior during cache failure. | Stale, missing, duplicate, and rebuild tests; evidence that cache loss does not destroy authoritative facts. |
| **3.5 Backup, Restore, and Corruption** | A backup is only a recovery capability after restoration has been tested against a recovery objective. | Define acceptable data loss and recovery time, automate backup verification, restore into isolation, and check application-level invariants afterward. | A timed restore drill, integrity checks, documented gaps, and an operator-readable recovery procedure. |

## Practice Sequence

1. Identify one critical fact in the shared system and every route that can change it.
2. Move one invariant from convention into a storage constraint without losing existing data.
3. Reproduce a partial multi-step update, then define and test its atomic boundary.
4. Run two conflicting operations concurrently and observe the chosen isolation behavior.
5. Perform an expand–migrate–contract change using production-shaped sample data.
6. Destroy a disposable copy of the store and complete a timed restoration.

## Shared-System Milestone

Make one critical data workflow survivable:

- declared source of truth and writer inventory;
- schema constraints for important invariants;
- transaction and isolation decision;
- compatible migration with validation and fallback;
- cache contract, if applicable;
- measured backup-and-restore evidence.

## Transfer to the Learner's Project

Choose the data whose loss or corruption would hurt most. Trace every writer, state its recovery objectives, and test one failure the project has previously assumed away.

## Phase Gate

The learner passes when they can:

- distinguish authoritative, replicated, cached, and computed data;
- connect each critical invariant to an enforcement point;
- explain the allowed outcome of two concurrent writes;
- evaluate a migration across mixed application versions;
- say what a rollback cannot undo;
- restore data and verify application meaning, not just file existence.

## Research Notes

The phase uses maintained database documentation for exact guarantees and formal consistency models for vocabulary. Product-specific defaults must always be checked in the learner's actual system. See finding 6 in [RESEARCH.md](../RESEARCH.md#6-data-reliability-is-about-declared-guarantees-not-database-presence).

---

[Phase 2](../02-how-codebases-hold-together/README.md) · **Phase 3** · [Phase 4: How Systems Communicate and Fail](../04-how-systems-communicate-and-fail/README.md)
