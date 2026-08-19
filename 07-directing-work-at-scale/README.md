# Phase 7: Directing Work at Scale

**Status:** curriculum outline

**Boundary introduced:** one accountable objective → bounded work graph → isolated execution → integrated result

## Purpose

Teach scale as a coordination problem. Learners decide when delegation helps, partition work along real interfaces, limit authority, and integrate evidence. Multiple agents are optional; accountable ownership is not.

## Phase Outcome

Direct one or more agents through a dependency-aware task graph, assign isolated ownership and permissions, require evidence-bearing handoffs, resolve cross-workstream conflicts, and maintain the resulting system after the feature moment has passed.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **7.1 Objectives, Decisions, and Task Graphs** | Work decomposes safely when outcomes, interfaces, dependencies, decisions, and integration points are explicit. | Convert a feature into a graph of bounded outcomes. Mark shared files, public contracts, irreversible decisions, unknowns, and the order in which evidence must arrive. | A graph with acceptance criteria, owners, dependencies, stop conditions, and one integration owner. |
| **7.2 When One Agent Beats Many** | Parallelism helps independent work; it adds communication cost and can amplify correlated mistakes. | Estimate coupling, conflict probability, review cost, context needs, and critical path. Compare a single-agent sequence with a multi-workstream topology before spawning work. | A delegation decision with predicted benefit and coordination cost, checked against the result afterward. |
| **7.3 Isolation, Permissions, and Handoffs** | Workstreams need separate ownership and least privilege so one local error does not silently become a system-wide change. | Assign explicit directories or interfaces, isolated branches/worktrees where appropriate, permitted tools, forbidden effects, and a handoff schema containing diff, checks, decisions, and risks. | No unexplained overlap, auditable actions, reproducible checks, and a handoff another agent or human can validate. |
| **7.4 Integration Is Its Own Engineering Task** | Individually correct changes can be jointly wrong when assumptions, interfaces, or timing conflict. | Re-read the combined diff, reconcile contracts, run broader checks, inspect generated and dependency changes, test cross-workstream failure paths, and keep the integration owner accountable. | Combined validation, resolved conflicts with rationale, architecture/security review, and an explicit accept/rework decision. |
| **7.5 Stewardship, Maintenance, and Mentorship** | A scaled result is successful only if future maintainers can understand, operate, and safely change it. | Remove temporary complexity, update decision and operating docs, assign follow-up ownership, inspect dependency/test health, and explain the system at the next person's altitude. | A maintenance review, updated runbook and decision record, closed or owned follow-ups, and a successful cold handoff. |

## Practice Sequence

1. Give the learner a feature with one genuinely separable investigation and one tightly coupled implementation.
2. Require a task graph and a reasoned one-agent versus multi-agent decision.
3. Run the separable work in isolation with a constrained handoff contract.
4. Seed two locally reasonable but incompatible interface assumptions.
5. Have the integration owner detect the mismatch through combined review and contract evidence.
6. Hand the result to a fresh reviewer or agent and record what context was missing.

## Shared-System Milestone

Deliver one coordinated improvement with:

- an objective and dependency-aware task graph;
- an explicit decision about agent count and topology;
- isolated ownership and permission boundaries;
- standardized, evidence-bearing handoffs;
- independent integration review and full-system checks;
- maintenance documentation and completed cold handoff.

The exercise may use one agent if the learner can show that additional agents would create more coordination cost than useful parallelism.

## Transfer to the Learner's Project

Choose a change that crosses at least two responsibilities. Decompose it, identify the interface between workstreams, and practice a handoff even if one agent performs both tasks sequentially.

## Phase Gate

The learner passes when they can:

- identify which work is genuinely independent and which only looks independent;
- defend the chosen number of agents and coordination topology;
- assign ownership without ambiguous shared-write scope;
- limit permissions and external effects per workstream;
- find a combined-system defect that local checks could miss;
- leave an operable system and a handoff that does not depend on private chat history.

## Research Notes

Current multi-agent studies show task- and topology-dependent benefits, including diminishing or negative returns. The course therefore evaluates coordination judgment rather than agent count. See finding 11 in [RESEARCH.md](../RESEARCH.md#11-multiple-agents-are-a-coordination-design-choice-not-a-maturity-badge).

---

[Phase 6](../06-how-software-stays-alive/README.md) · **Phase 7** · [Phase 8: Proving Reliability](../08-proving-reliability/README.md)
