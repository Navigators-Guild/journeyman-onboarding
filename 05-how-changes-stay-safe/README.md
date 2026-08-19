# Phase 5: How Changes Stay Safe

**Status:** curriculum outline

**Boundary introduced:** proposed change → falsification → integration → release → rollback

## Purpose

Turn testing from “ask the agent to add tests” into the design of evidence. Learners choose checks according to the claim, challenge whether the checks can detect a defect, and carry that evidence through integration and release.

## Phase Outcome

Direct an agent to build a risk-based verification strategy using example, integration, property, fuzz, and mutation techniques; automate it in continuous integration; review the whole change; and release with compatibility and rollback evidence.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **5.1 Claims, Oracles, and Test Boundaries** | A test is meaningful only when its expected result comes from a requirement or independent model and it can fail for a relevant defect. | Build a claim-to-check matrix. Separate fast component checks, boundary integration, full workflow, static analysis, and human review by the risk each addresses. | Demonstrate a seeded defect that the intended check catches; identify important claims with no affordable automated oracle. |
| **5.2 Properties, Generators, and Fuzzing** | Examples sample cases; properties describe relationships that should hold across a space of cases. | Derive invariants, round trips, monotonicity, equivalence, and metamorphic relations. Constrain generators to useful valid and invalid regions, preserve minimal failures as regressions. | A property or fuzz run that finds or could find more than the hand-written examples, with reproducible failure inputs. |
| **5.3 Test the Tests with Mutation** | A green suite may never observe the behavior it claims to protect. Deliberate code changes can expose weak assertions. | Mutate a bounded critical slice, classify surviving changes, strengthen only valuable checks, and record equivalent or irrelevant mutants rather than chasing a vanity score. | Killed consequential mutants, reviewed survivors, and a reasoned residual gap. |
| **5.4 Continuous Integration and Whole-Diff Review** | Evidence is dependable when it is reproducible from declared inputs and the complete change is inspected in context. | Create one canonical validation path, run it in a clean environment, inspect formatting/types/lints/tests/build/docs/generated files, and compare the diff with scope. | A clean CI run, reviewed diff, dependency/config changes called out, and failures that block merging. |
| **5.5 Compatibility, Release, and Rollback** | A release changes another system's assumptions; rollback is a designed path, not a hopeful command. | Define consumers, versioning, migration order, feature exposure, health criteria, rollback trigger, and irreversible effects. Stage the rollout according to blast radius. | Release notes, compatibility checks, artifact identity, staged health evidence, and a rehearsed rollback or forward-recovery plan. |

## Practice Sequence

1. Audit a shallow shared-system test and identify where its oracle copies the implementation.
2. Rewrite the claim independently and seed a plausible defect.
3. Add a property or fuzz target around a high-dimensional input boundary.
4. Run mutation testing on a bounded critical slice and analyze a surviving mutant.
5. Reproduce the full validation path from a clean checkout or environment.
6. Stage a release, violate a health criterion, and perform the planned recovery.

## Shared-System Milestone

Produce a merge- and release-ready change containing:

- a risk-ranked claim-to-check matrix;
- meaningful component and integration evidence;
- at least one generative technique where appropriate;
- a bounded mutation analysis;
- reproducible continuous integration;
- whole-diff review and compatibility notes;
- staged release and rollback evidence.

## Transfer to the Learner's Project

Choose a feature currently protected only by happy-path tests. Build its claim-to-check matrix, improve one weak oracle, and demonstrate the improved suite by making it catch a deliberate defect.

## Phase Gate

The learner passes when they can:

- explain what each check establishes and does not establish;
- identify a tautological or implementation-coupled test;
- select a property or fuzz boundary for a reason;
- interpret mutation results without optimizing blindly for a score;
- reconcile targeted success with broader repository failure;
- stop or reverse a release when stated evidence is missing.

## Research Notes

The phase combines established generative-testing techniques, empirical mutation-testing research, and recent evidence about the gap between benchmark success and merge readiness. See findings 4 and 8 in [RESEARCH.md](../RESEARCH.md#findings-that-shape-the-course).

---

[Phase 4](../04-how-systems-communicate-and-fail/README.md) · **Phase 5** · [Phase 6: How Software Stays Alive](../06-how-software-stays-alive/README.md)
