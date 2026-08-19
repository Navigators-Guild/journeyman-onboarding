# Phase 8: Proving Reliability

**Status:** assessment design outline; rubric requires pilot validation

**Boundary introduced:** system claims → independent evidence → adversarial challenge → responsible handoff

## Purpose

Require the learner to integrate the entire path on a real, independently chosen project. Agents remain available. The assessment measures direction, modeling, judgment, verification, recovery, and explanation—not manual code production.

## Phase Outcome

Harden a bounded vibecoded system and defend a reliability case that connects important user and operator claims to design decisions, implementation changes, falsifying checks, operational exercises, and honestly stated residual risks.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **8.1 Choose the Claim, Boundary, and Stake** | Reliability is always reliability for a defined behavior, environment, user, and consequence. | Map candidate projects, users, critical workflows, data, dependencies, deployment context, and harms. Propose a scope large enough to integrate the phases but small enough to verify. | Approved scope, non-goals, stakeholder or user proxy, critical claims, and completion/stop criteria. |
| **8.2 Establish the Baseline and Assurance Plan** | Improvement cannot be demonstrated without a reproducible baseline and a plan linking risk to evidence. | Reconstruct architecture, state, trust, data, operational boundaries, current checks, and known failures. Rank risks and create a claim-to-evidence matrix before implementation. | Reproducible baseline, system and threat models, risk register, and assurance plan reviewed for blind spots. |
| **8.3 Run Bounded Hardening Cycles** | Each cycle should reduce a named risk while preserving an inspectable evidence chain. | For one risk at a time, compare designs, record the authorized choice, implement in a bounded diff, run targeted and broad checks, review, and update the dossier. | Requirement → decision → diff → checks → review → residual-risk trace for every accepted cycle. |
| **8.4 Challenge and Operate the System** | A reliability case needs evidence from unfavorable conditions, not only demonstrations arranged to succeed. | Design independent adversarial cases, inject boundary failures, test recovery and rollback, observe service behavior, and let another reviewer challenge assumptions. | Failure exercise, restore or rollback timing, telemetry trail, independent findings, and disposition of each finding. |
| **8.5 Defend, Hand Off, and Reflect** | Responsible ownership includes explaining why the evidence is sufficient for this use—and where it is not. | Assemble the reliability case, remove unsupported claims, prepare a cold-start runbook, and rehearse questions about trade-offs, rejected options, and residual risk. | Working demonstration, evidence dossier, decision records, operator/developer handoff, defense, and structured reflection. |

## Practice Sequence

1. Review the shared-system dossier and perform a short mock defense to expose missing evidence.
2. Propose two possible independent projects and select one by risk, scope, access, and testability.
3. Establish the baseline and assurance plan before authorizing hardening work.
4. Complete bounded cycles, updating the dossier after each accepted change.
5. Invite an independent challenge, run the failure and recovery exercises, and resolve findings.
6. Deliver the final defense and cold handoff, then record how the learner's model changed.

## Shared-System Milestone

The shared application is a rehearsal, not the final submission. Freeze its reliability dossier, give it to a reviewer without private conversation history, and use their unanswered questions to improve the final-project plan and handoff standard.

## Transfer to the Learner's Project

The independently chosen project is the phase work. It must be meaningfully different from the guided application and contain enough state, boundaries, or operational consequence to require integrated judgment. A reviewer approves the scope before hardening begins.

## Required Reliability Case

The final dossier must contain:

- project scope, users, environment, non-goals, and authorization boundary;
- repository, architecture, data, interaction, deployment, and threat models;
- behavior contracts, invariants, critical failure paths, and risk ranking;
- decisions with alternatives and consequences;
- bounded change history with reviewed diffs;
- claim-to-evidence matrix and reproducible validation commands;
- data recovery, release rollback or forward-recovery, and incident evidence;
- dependency, configuration, credential, and agent/tool boundaries;
- independent review findings and their disposition;
- residual risks, operating limits, and next actions;
- a handoff that works without access to private prompts or conversations.

## Proposed Assessment Dimensions

| Dimension | Weight | What strong evidence looks like |
|---|---:|---|
| Grounding and scope control | 15% | Repository facts are traceable; non-goals and authority are respected; changes stay bounded. |
| System modeling and risk | 20% | State, boundaries, invariants, failure paths, data, and threats agree with observed behavior. |
| Decisions and architecture | 15% | Alternatives are credible; choices follow constraints; compatibility and reversibility are explicit. |
| Verification quality | 25% | Oracles are independent; checks cover important risks; adversarial and broader evidence can falsify claims. |
| Security, operations, and recovery | 15% | Permissions are limited; release is observable; failure is detected; recovery is practiced and measured. |
| Explanation and handoff | 10% | Another person can operate and change the system; uncertainty and residual risk are stated plainly. |

The proposed pass mark is 75%, with no score below 60% in **verification quality** or **security, operations, and recovery**. These weights and thresholds are hypotheses until pilot work establishes that raters can apply them consistently and that they distinguish the intended capability.

## Assessment Conditions

- Agents, documentation, search, and repository tools are allowed.
- Consequential actions still require authorization and least privilege.
- The learner must make predictions and consequential decisions in their own words.
- Agent transcripts may support reflection but are neither required public artifacts nor proof of competence.
- Some adversarial cases are withheld until the challenge session.
- A second reviewer samples the dossier and challenges at least one unsupported or under-supported claim.
- The learner may revise after feedback; reliable development includes responding to findings.

## Phase Gate

The learner completes the path when the system and dossier meet the rubric floor and the learner can:

- navigate from a critical claim to the code, checks, runtime evidence, and residual risk;
- explain why a plausible alternative was rejected;
- diagnose a new failure from observable evidence while directing the agent;
- stop an unsafe action or release despite agent confidence;
- recover the system within the stated objective or explain the measured gap;
- transfer ownership without depending on hidden context.

Course completion should not be advertised as a professional certification until the rubric, reviewer agreement, transfer task, and assessment process have been piloted and published.

## Research Notes

The phase uses authentic, project-based evidence because it resembles the work being claimed. It uses explicit dimensions and multiple evidence forms because competency-assessment reviews warn that vague constructs and self-report are weak foundations. Structured reflection is included as a learning aid, not a substitute for system evidence. See finding 12 and the validation plan in [RESEARCH.md](../RESEARCH.md#12-assessment-should-resemble-the-work-and-collect-more-than-self-report).

---

[Phase 7](../07-directing-work-at-scale/README.md) · **Phase 8** · [Course overview](../README.md)
