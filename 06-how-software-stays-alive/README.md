# Phase 6: How Software Stays Alive

**Status:** curriculum outline

**Boundary introduced:** built artifact → trusted release → operated service → incident recovery

## Purpose

Expand responsibility beyond the development session. Learners direct security, deployment, telemetry, service objectives, and incident response as one operating system—and treat the coding agent and its tools as part of that system.

## Phase Outcome

Direct an agent to model threats and trust boundaries, enforce identity and authorization, constrain agent/tool access, protect the build and release path, deploy observable software, and lead evidence-based recovery from an incident.

## Module Outline

| Module | System principle | Direction to the agent | Required evidence |
|---|---|---|---|
| **6.1 Threats, Assets, and Trust Boundaries** | Security starts with what must be protected, from whom, across which boundary, and with what impact—not a generic checklist. | Inventory assets, actors, entry points, data flows, privileges, abuse cases, and assumptions. Rank threats and propose controls at prevention, detection, and recovery layers. | A reviewed threat model connected to concrete requirements and residual risks. |
| **6.2 Identity, Authorization, and Secrets** | Authentication names an actor; authorization limits an action; neither belongs only in the user interface. | Trace identity across every boundary, centralize policy where practical, default to denial, test object- and action-level access, and keep secrets out of prompts, code, logs, and artifacts. | Positive and negative authorization tests, secret scanning, rotation/revocation procedure, and auditable decisions. |
| **6.3 Agent, Tool, and Supply-Chain Security** | Retrieved text, plugins, tools, packages, build inputs, and generated changes are untrusted until authorized and verified. | Minimize permissions, separate read from write and deploy authority, inspect instructions and dependency changes, pin or attest important inputs, and require human approval for consequential external effects. | Permission inventory, adversarial instruction exercise, dependency review, provenance or attestation evidence, and blocked unauthorized action. |
| **6.4 Deployment and Configuration Change** | Deployment changes a running system under real load; configuration is executable behavior with its own lifecycle. | Separate build from release, validate environment assumptions, stage exposure, define health and abort criteria, preserve artifact identity, and plan rollback around state compatibility. | Reproducible artifact, environment validation, staged deployment observations, and recovery drill. |
| **6.5 Observability, Service Objectives, and Capacity** | Telemetry is useful when it answers user and operator questions; an objective turns those signals into an operating decision. | Define user-critical indicators, structured logs, metrics, traces, correlation, retention, and privacy. Set an objective and alerts tied to actionable symptoms; test capacity before exhaustion. | A failure traced across signals, an actionable alert, an objective calculation, and a measured saturation point. |
| **6.6 Incidents, Recovery, and Learning** | Incidents require practiced roles, safe stabilization, an evidence timeline, and system improvements—not individual blame or improvised heroics. | Define severity, roles, communications, containment options, decision logs, and escalation. Run a scenario, preserve evidence, and turn contributing conditions into owned follow-up work. | Timed incident exercise, recovery against objectives, post-incident analysis, and verified corrective action. |

## Practice Sequence

1. Threat-model the shared system and include the agent's own tools and credentials.
2. Reproduce an object-level authorization flaw and add a negative test at the enforcing boundary.
3. Feed the agent untrusted repository text that requests an unauthorized action; verify the action is rejected and reported.
4. Generate a traceable artifact and stage a configuration change with abort criteria.
5. Trigger a user-visible failure and follow it from alert through logs, metrics, and traces.
6. Run an incident exercise, recover the service, and complete one corrective action.

## Shared-System Milestone

Operate a hardened release with:

- a threat model and residual-risk register;
- tested authorization and secret lifecycle;
- least-privilege agent/tool boundaries;
- reviewed dependencies and traceable build artifact;
- staged deployment and rollback criteria;
- user-centered service objective and useful telemetry;
- an incident drill, post-incident analysis, and completed follow-up.

## Transfer to the Learner's Project

Choose the project's most consequential action. Trace who or what can trigger it, with which credentials, through which tools and dependencies, and how misuse or failure would be detected and reversed.

## Phase Gate

The learner passes when they can:

- distinguish an asset, threat, vulnerability, control, and residual risk;
- demonstrate a denied action rather than only a successful login;
- limit agent authority independently of the wording of a prompt;
- identify the exact artifact and configuration running in an environment;
- connect a user symptom to actionable telemetry and a service objective;
- stabilize and recover during a practiced incident without hiding uncertainty.

## Research Notes

This phase combines stable secure-development and supply-chain standards with rapidly evolving agentic-security guidance, plus maintained observability and SRE practices. Emerging threat lists are taught as prompts for analysis, not prevalence rankings. See findings 9 and 10 in [RESEARCH.md](../RESEARCH.md#findings-that-shape-the-course).

---

[Phase 5](../05-how-changes-stay-safe/README.md) · **Phase 6** · [Phase 7: Directing Work at Scale](../07-directing-work-at-scale/README.md)
