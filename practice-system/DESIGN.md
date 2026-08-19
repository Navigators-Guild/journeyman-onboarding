# Waystation Shared Practice System Design

**Decision status:** ready for prototype

**Last reviewed:** 2026-08-19

## Objective

Create one realistic, intentionally brittle application that learners can investigate and harden from Phase 0 through Phase 7 while directing coding agents. The system must make the course's abstract concepts observable without requiring real credentials, real personal data, or production infrastructure.

Waystation succeeds as a teaching system when a learner can:

- see a convincing happy path before understanding the implementation;
- discover that the happy path supports claims the system cannot yet justify;
- repair one bounded risk without discarding the existing application;
- preserve earlier decisions and evidence through later phases;
- reproduce failures safely and reset the lab;
- transfer the principle to a different project rather than memorizing a Waystation fix.

## Explicit Exclusions

The first course baseline will not include:

- payments, real email or SMS, social login, or cloud credentials;
- real names, addresses, contact details, or equipment records;
- deliberately vulnerable third-party package versions;
- a public multi-tenant deployment exposed to the internet;
- hidden malware, destructive scripts, or exercises that escape the repository;
- a prescribed “perfect architecture” that every learner must reproduce;
- phase completion based only on matching a reference diff.

The system teaches reliability engineering. It is not a security capture-the-flag environment or a framework tutorial.

## Why This Domain

Equipment lending is understandable without specialist knowledge, but it naturally creates the engineering pressures the path needs:

- equipment and reservations have state and invariants;
- two members can compete for the same period;
- check-out and return require authorization and an audit trail;
- data must survive interruption and schema change;
- notifications can be delayed, duplicated, or lost;
- maintenance status affects availability;
- operators need to detect and recover from bad releases and incidents.

A learner can reason about these consequences in ordinary language before encountering their implementation.

## Users and Critical Workflows

### Member

1. Browse active equipment and availability.
2. Request a reservation for a time range.
3. View or cancel their own future reservations.
4. Receive a locally recorded confirmation or cancellation notice.

### Steward

1. Confirm or reject requests according to the lending policy.
2. Check reserved equipment out to the correct member.
3. Record returns and move damaged equipment into maintenance.
4. View the operational history needed to resolve a dispute.

### Operator

1. Start, configure, inspect, back up, restore, and upgrade the service.
2. Observe user-critical behavior and background work.
3. Contain and recover from a failed request, worker, migration, or release.

The baseline can use simulated identities selected from fixture data. Authentication mechanics arrive only when the relevant phase can examine them responsibly.

## Domain Model

The implementation may refine names, but it must preserve the following concepts:

| Concept | Authoritative facts | Important relationships |
|---|---|---|
| Member | Identifier, display name, active status | Owns reservations; may receive recorded notifications |
| Equipment | Identifier, name, category, lifecycle state | Has reservations, checkouts, and maintenance events |
| Reservation | Member, equipment, start/end, status, creation time | May lead to one checkout; conflicts with overlapping active reservations |
| Checkout | Reservation, steward, checked-out time, returned time | At most one open checkout per equipment item |
| Maintenance event | Equipment, reason, opened/closed times | Unresolved maintenance makes equipment unavailable |
| Notification job | Event identity, recipient, template, status, attempts | Must tolerate retry without producing unintended duplicates |
| Audit event | Actor, action, target, time, correlation identifier | Supports diagnosis; must not contain secrets |

### Candidate invariants

These are domain requirements, not implementation instructions:

1. An end time must be later than its start time.
2. Retired equipment cannot receive a new reservation.
3. An equipment item cannot have overlapping confirmed reservations.
4. An equipment item cannot have more than one open checkout.
5. A checkout must refer to a confirmed, currently applicable reservation.
6. Only a steward may check equipment out, accept a return, or change maintenance state.
7. A member may view or cancel only their own reservation unless acting as a steward.
8. A completed domain action has one stable event identity for notification and audit processing.
9. Failure to deliver a notification must not reverse an otherwise committed reservation.
10. Authoritative facts must remain reconstructable after loss of any derived cache or read model.

The brittle baseline will violate or weakly enforce some of these rules. The exact enforcement decisions belong to the learner exercises and must not all be pre-solved by the starter architecture.

## Runtime Boundary

The smallest system that supports the whole course has four runtime responsibilities:

```text
Browser or API client
        |
        v
Waystation application -----> SQLite source of truth
        |                              |
        | commits notification job     | backup / restore
        v                              v
Local notification worker -----> Recorded-message sink

Application and worker -----> Local logs, metrics, and traces
```

The browser exercises public and steward workflows. The application owns HTTP behavior and domain orchestration. SQLite supplies a realistic local transaction and migration boundary. A separate worker makes delay, duplication, retry, and observability visible. The message sink records fictional notifications as inspectable local data rather than contacting an external service.

## Preferred Implementation Shape

Use a Rust workspace, building on the Apprentice path's existing Rust toolchain, with SQLite and server-rendered HTML. Avoid a separate JavaScript build unless a later learning objective genuinely needs one.

The baseline should begin with too much responsibility concentrated in one application crate. It may have sensible files, but it should not pre-solve the Phase 2 ownership exercise by presenting an ideal domain architecture.

Proposed learner-visible shape:

```text
README.md
Cargo.toml
docs/
  PRODUCT.md
  OPERATIONS.md
fixtures/
  waystation-demo.*
migrations/
src/
  main.rs
  catalog.rs
  reservations.rs
  storage.rs
  notifications.rs
tests/
  happy_path.rs
tools/
  reset-lab.*
```

Exact frameworks and dependency versions are intentionally deferred to the prototype preflight. That review must select maintained versions from primary documentation, record the supported Rust version, and prove clean setup on the supported learner platforms.

### Supported environment

- Primary: current stable Rust on Linux and Windows through WSL.
- Secondary: macOS, verified before a course release.
- No required container runtime for the first four phases.
- Optional container packaging may be introduced for deployment exercises later.

## Curriculum Failure Map

The baseline contains all major teaching pressures from the beginning so learners maintain one evolving system. Chapters reveal them progressively and scope the work; they do not inject a new arbitrary defect after each successful phase.

| Phase | Visible pressure | Seeded weakness class | Required repair evidence |
|---|---|---|---|
| 0: Models | A handoff description disagrees with the repository | Incomplete documentation, surprising runtime boundary, unsupported claims | Grounded repository map, explicit assumptions, baseline results |
| 1: Programs | Rare actions create contradictory equipment state | Primitive strings/flags, scattered validation, mixed effects and calculation, flattened errors | State model, enforced invariant, error-path and boundary evidence |
| 2: Codebases | A policy change touches unrelated files | Leaked responsibility, storage details crossing boundaries, direct configuration reads, duplicated rules | Responsibility map, bounded refactor, contract and dependency evidence |
| 3: Data | Interrupted and concurrent operations corrupt meaning | Weak constraints, multi-step non-atomic writes, unsafe migration, untested restore, disposable data treated as authoritative | Constraint and concurrency tests, compatible migration, timed restore |
| 4: Communication | A lost response or worker retry duplicates an effect | Missing idempotency, broad retry, no deadline budget, race-prone reservation, unbounded queue behavior | Timeline model, duplicate/loss tests, bounded retry, overload and reconciliation evidence |
| 5: Safe change | The suite stays green when important behavior is broken | Happy-path-only tests, implementation-copied oracles, missing integration checks, non-reproducible release steps | Claim-to-check matrix, seeded-defect detection, CI and rollback evidence |
| 6: Operations | A plausible request crosses the wrong authority or becomes invisible | Route-level authorization gap, over-broad agent/runtime permissions, unsafe logging/configuration, weak telemetry and incident procedure | Threat model, denied-action tests, provenance, observable failure and recovery drill |
| 7: Scale | Two correct-looking changes conflict during integration | Shared ownership, implicit interface assumptions, incomplete handoffs, local-only verification | Task graph, isolation, evidence-bearing handoffs, combined-system review |

### Seeded-failure rules

Every intentional weakness must have:

1. A learning objective and owning phase.
2. A safe, deterministic reproduction using fixture data.
3. A plausible happy path explaining why it escaped notice.
4. Observable user or operator impact.
5. A facilitator oracle independent of the flawed implementation.
6. A bounded repair envelope; a full rewrite must not be the easiest answer.
7. A regression check that can remain in the learner's evolving suite.
8. A reset path tested from a clean clone.

Do not seed nondeterministic “flakiness” without a deterministic harness. Do not make the lesson depend on guessing an undocumented trick. Do not add a vulnerability that becomes dangerous merely because a learner runs the default command.

## Repository and Release Model

Waystation should live in its own repository so course text and application history can evolve independently while releases remain traceable.

The preferred learning flow is:

1. The course pins a tested Waystation baseline tag.
2. The learner creates a personal hardening branch from that tag.
3. Every phase builds on the learner's earlier accepted work.
4. Evidence packets record commits and commands rather than reference-solution similarity.
5. A reset command restores disposable runtime data without rewriting Git history.
6. A documented recovery tag lets a learner restart only when their repository is genuinely unrecoverable.

Maintainer-only scenario oracles may live in the course release process, but normal learner checks must be understandable and runnable in the learner repository. Reference implementations are review aids, not the grading oracle.

### Credible alternative: independent phase snapshots

Each phase could begin from its own known repository snapshot. This makes workshops easier to support and ensures every learner sees the same defect. It also discards the consequences of earlier decisions, teaches less about regression and maintenance, and turns the system into a sequence of puzzles.

Use snapshots only for recovery, short demonstrations, and facilitator validation. Keep the continuous hardening branch as the default.

### Credible alternative: TypeScript full-stack application

A TypeScript application would make browser behavior easy to extend and expose runtime type-boundary failures clearly. It would add a second ecosystem after the Rust-oriented Apprentice path, a JavaScript build surface that is not central to the early lessons, and more dependency churn.

Retain TypeScript as a fallback if the Rust prototype cannot meet setup-time and cross-platform gates. The domain and failure curriculum do not depend on Rust.

## Learner and Facilitator Evidence

### Learner repository contains

- honest product behavior and setup documentation;
- fictional fixture data and safe reset tooling;
- the intentionally shallow baseline checks;
- observable local logs and recorded notification output;
- no file named “solutions” and no hidden credential requirement.

### Course release process retains

- a manifest connecting each weakness class to its learning objective;
- deterministic scenario oracles used to validate the baseline;
- known repair envelopes and interactions between phases;
- clean-clone setup measurements on supported platforms;
- a record of which course version pins which Waystation tag.

Publishing those maintainer artifacts later is compatible with the course. Secrecy is not the source of rigor; evidence and transfer are.

## Failure and Recovery Design

- The default server binds only to a local interface.
- The default message adapter writes only to a disposable local sink.
- Each exercise can use a named fixture database copied from a read-only seed.
- Reset refuses paths outside the recognized lab-data directory.
- Migration drills create a backup before destructive steps and run on disposable copies.
- Concurrency exercises use a bounded deterministic harness rather than uncontrolled load.
- Security exercises test policy with fictional identities and no real secrets.
- Incident exercises expose a symptom, evidence trail, and recovery objective without depending on an external outage.

## Delivery Plan

### Increment 1: executable skeleton

Build catalog, reservation, steward checkout/return, SQLite persistence, fictional fixtures, and recorded notifications. Supply one documented start command and one safe reset command.

Completion evidence:

- clean setup on Linux/WSL from declared prerequisites;
- a member can complete the happy path through the browser;
- state survives an application restart;
- the notification sink records rather than sends;
- reset restores the exact fixture baseline;
- repository-wide checks pass.

### Increment 2: curriculum harness

Add deterministic scenario drivers and maintainer oracles for each failure class without exposing real systems or making normal startup dangerous.

Completion evidence:

- every seeded weakness is reproduced from a clean baseline;
- every scenario names its user/operator impact and owning phase;
- scenarios are bounded in runtime and reset successfully;
- one defect does not accidentally invalidate an earlier phase's core exercise.

### Increment 3: Phase 0 release

Finalize the inaccurate handoff packet, repository-map exercise, sample evidence packet, and course-to-baseline version pin.

Completion evidence:

- a fresh reviewer can complete the chapter without unwritten setup knowledge;
- the agent's repository map can be checked against paths and runtime output;
- the exercise has at least one plausible inference that repository evidence disproves;
- no application change is required to pass the chapter.

### Increment 4: phased validation

Pilot each subsequent phase against a preserved copy of the previous accepted state. Track setup friction, false confidence, unintended solution paths, repair interactions, and transfer to another repository.

Completion evidence:

- learner and facilitator checks agree on the observed failure;
- the repair does not pre-solve or destroy later learning boundaries;
- the learner can apply the same principle to a non-Waystation project;
- findings update both the baseline and relevant chapter.

## Decisions Still Open at Prototype Time

The prototype may decide these reversibly after measurement:

- specific HTTP, template, SQLite, migration, and telemetry libraries;
- whether the worker starts as a separate process or a separately invokable mode;
- exact fixture format and cross-platform reset implementation;
- supported browser versions;
- which checks run in the learner's fast path versus the release validation path.

These are implementation choices, not reasons to leave the system boundary or learning contract vague.

## Architecture Verdict

**Ready for prototype.** The domain supports every planned learning boundary, the local-only design limits risk, and the continuous repository preserves authentic maintenance pressure. The largest residual risk is that Rust setup or compile time distracts from the systems lessons; Increment 1 must measure that before the stack becomes a long-lived course dependency.

---

[Practice-system overview](README.md) · [Course overview](../README.md)
