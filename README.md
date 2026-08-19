# The Guild Journeyman Learning Path

**Turning vibecoders into reliable, agent-directed developers.**

You can already make software with an AI coding agent. You can describe an idea, watch files appear, run the result, and refine it until the demo feels right. That is a real capability. It is also where many people get stuck.

A convincing demo is not necessarily dependable software. The difference is not whether you typed the code yourself. The difference is whether you can describe the system, direct consequential changes, demand meaningful evidence, recognize risk, and recover when reality disagrees with the plan.

That is what this path teaches.

## The Premise

Traditional programming education usually begins with syntax: variables, loops, functions, data structures, and increasingly complicated programs written by hand. That route works for some people and fails others whose strength is reasoning about goals, systems, constraints, and trade-offs.

This path uses a different interface.

The coding agent writes the implementation. You learn the programming and developer concepts needed to direct it well. Every concept is taught as a system principle, a decision you need to understand, an instruction you can give the agent, and evidence you can use to judge the result.

You will not be asked to memorize syntax or prove that you can work without an agent. You will be asked to think clearly, make trade-offs, authorize actions responsibly, and show why the resulting software deserves confidence.

Vibecoding is the starting point, not an insult. Journeyman practice begins when intuition is joined by explicit models and verification.

## Who This Is For

This course is for systems thinkers who use coding agents as their primary implementation tool. You may struggle with syntax-first instruction while being good at understanding how parts fit together, spotting missing requirements, anticipating failure, or steering complex work.

You should arrive able to:

- Use a coding agent inside an authorized project directory
- Describe desired behavior and refine an ambiguous request
- Use Git to inspect and preserve changes
- Run commands and share exact errors with the agent
- Compare a result with written acceptance criteria
- Treat agent claims as hypotheses that require evidence

Completing the Guild Apprentice path is one way to build that foundation, but equivalent experience is valid.

## What You Are Becoming

A Journeyman is not a person who knows every language feature. A Journeyman can take responsibility for a software system while using agents for implementation.

By the end of this path, you should be able to:

- Turn an idea into explicit behavior, constraints, invariants, and failure cases
- Ask an agent to map an unfamiliar repository before it changes anything
- Direct modular designs with clear responsibilities and interfaces
- Reason about state, data, persistence, concurrency, networks, and security
- Require tests whose expected results come from requirements rather than the implementation
- Evaluate dependencies, migrations, releases, and compatibility risks
- Deploy software with useful telemetry, recovery procedures, and rollback plans
- Coordinate multiple bounded work streams without losing integration quality
- Explain what the available evidence establishes and what remains uncertain
- Maintain and improve software after the first successful release

## The Division of Responsibility

The agent is not a disposable typist, and it is not the accountable owner. Reliable agent-directed development depends on a clear division of responsibility.

| You own | The agent can do | Evidence decides |
|---|---|---|
| Purpose and intended users | Inspect repositories and documentation | Whether observed behavior matches the requirement |
| Requirements and constraints | Propose designs and trade-offs | Whether checks exercise the important risks |
| Risk tolerance and authorization | Implement code, tests, and configuration | Whether the full change integrates successfully |
| Product and domain judgment | Run tools and explain their output | Whether failures are observable and recoverable |
| Acceptance of residual risk | Search for defects and alternatives | Whether the result is ready for its intended use |

The agent may help with every item in the first column. You remain responsible for deciding whether its proposal matches reality and whether an action is authorized.

## How the Course Teaches

Every chapter follows the same learning loop:

1. **Understand the principle.** Learn the developer concept in plain systems language.
2. **See why it exists.** Examine how plausible vibecoded software fails without it.
3. **Model the system.** Identify the state, boundaries, responsibilities, and failure paths involved.
4. **Direct the agent.** Give it a scoped brief that expresses the principle and required evidence.
5. **Inspect the change.** Review what changed, what assumptions were made, and what was left alone.
6. **Verify the claim.** Run checks that could reveal a wrong implementation.
7. **Try to break it.** Use adversarial cases, fault injection, or review to challenge the happy path.
8. **Preserve the evidence.** Record decisions, results, limitations, and the next action.

The reusable structure for authors and contributors lives in [CHAPTER_TEMPLATE.md](CHAPTER_TEMPLATE.md). The evidence review and its limitations live in [RESEARCH.md](RESEARCH.md).

## Course Map

The precise chapter list will evolve as the course is researched and piloted. The learning progression is organized around expanding system boundaries.

### [Phase 0: From Vibes to Models](00-from-vibes-to-models/README.md)

Move from “it seems to work” to a concrete model of behavior, constraints, assumptions, and evidence. Learn to make the agent inspect before editing and distinguish repository facts from guesses.

### [Phase 1: How Programs Hold Together](01-how-programs-hold-together/README.md)

Learn state, types, invariants, control flow, functions, errors, and data structures as design tools. Direct the agent to make valid behavior clear and invalid behavior difficult to express.

### [Phase 2: How Codebases Hold Together](02-how-codebases-hold-together/README.md)

Learn modules, interfaces, dependencies, configuration, architecture, and refactoring. Direct changes that preserve clear ownership and keep unrelated concerns from becoming tangled.

### [Phase 3: How Data Survives](03-how-data-survives/README.md)

Learn persistence, schemas, migrations, transactions, atomicity, caching, and recovery. Decide what the source of truth is and how the system protects it when work is interrupted.

### [Phase 4: How Systems Communicate and Fail](04-how-systems-communicate-and-fail/README.md)

Learn APIs, networks, timeouts, retries, idempotency, concurrency, queues, and partial failure. Replace optimistic assumptions with explicit contracts and bounded recovery behavior.

### [Phase 5: How Changes Stay Safe](05-how-changes-stay-safe/README.md)

Learn unit, integration, property, fuzz, and mutation testing; continuous integration; compatibility; review; releases; and rollback. Match each verification method to the claim it can actually support.

### [Phase 6: How Software Stays Alive](06-how-software-stays-alive/README.md)

Learn threat modeling, authorization, secrets, agent and tool security, deployment, observability, service objectives, incident response, and postmortems. Build software that can be understood and recovered after it leaves the development session.

### [Phase 7: Directing Work at Scale](07-directing-work-at-scale/README.md)

Learn task graphs, agent roles, permission boundaries, isolated parallel work, integration, design review, handoffs, maintenance, and mentorship. Increase leverage without increasing the blast radius blindly.

### [Phase 8: Proving Reliability](08-proving-reliability/README.md)

Take an independently chosen vibecoded project and harden it into a system whose important claims are supported by inspectable evidence. Agents remain available throughout the assessment. Direction, judgment, verification, and recovery are the skills being evaluated.

## The Shared Practice System

The guided work will use an intentionally vibecoded application that looks convincing but is brittle beneath the surface. It will contain realistic weaknesses such as tangled responsibilities, weak validation, accidental invalid states, fragile persistence, shallow tests, unsafe configuration, race conditions, and poor operational visibility.

You will not throw it away and ask for a clean rewrite. You will direct an agent to map it, stabilize it, and improve it in bounded steps. Each phase will introduce a principle at the moment the system creates a need for it. You will then apply the same principle to one of your own projects so the lesson transfers beyond the shared exercise.

## Assessment With Agents

Agents are allowed throughout the course, including the final assessment. This course does not use agent-free coding as a proxy for competence.

Assessment asks whether you can:

- Ground the agent in the actual repository and current objective
- Expose assumptions before they become implementation decisions
- Compare credible designs and choose according to stated constraints
- Limit scope, tools, credentials, and external effects
- Demand checks capable of falsifying the implementation
- Detect tautological tests, unsupported claims, and unnecessary complexity
- Diagnose failures using observable evidence
- Explain the system and the accepted residual risks in plain language

The durable evidence is the chain connecting a requirement to a decision, a change, a verification result, a review, and a documented risk. Prompt transcripts may support reflection, but learners should not be required to publish secrets, private conversations, proprietary code, or personal data.

## What This Course Is Not

- A syntax memorization course
- A collection of magic prompts
- A promise that one model or tool always produces correct software
- A replacement for qualified security, legal, safety, or domain review
- A guarantee of employment, mastery, certification, or error-free systems
- Permission to give agents unrestricted access or accept changes without inspection

The goal is not to remove the human from development. It is to put human systems thinking where it has the most leverage.

## Project Status

This repository is at the curriculum-design stage. The course manifesto, researched phase outlines, chapter template, and initial evidence review are present. The shared practice system, full chapters, learner materials, assessment instruments, and pilot validation remain to be developed in reviewable increments.

The manifesto is the contract: teach the principle, show what to tell the agent, and require evidence that the result holds up.
