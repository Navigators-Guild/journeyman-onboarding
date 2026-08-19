# The Repository Is Evidence

**Chapter status:** authored draft; the Waystation baseline is not yet released

An agent can begin coding from a sentence. That does not mean the sentence describes the system in front of it.

Repositories accumulate history. The README may describe an earlier design. A test may cover only the happy path. A configuration file may override the default you saw in code. An uncommitted edit may belong to somebody else. A command may work on one machine because of a tool or environment value nobody recorded.

Your first Journeyman habit is therefore simple: investigate before you authorize change.

## What You Will Be Able to Do

By the end of this chapter, you will be able to:

- direct an agent to map the part of a repository relevant to a request;
- distinguish requirements, repository facts, runtime observations, inferences, and unknowns;
- verify important claims by following them to files and command output;
- produce a compact repository map without changing application behavior;
- explain where the map is incomplete and what evidence would strengthen it.

You are not trying to memorize the repository. You are learning how to build a trustworthy working model when a change requires one.

## The Principle

A prompt describes intent and context. The repository contains evidence of the current implementation. Runtime observations show what happened in one environment under particular conditions. None of those sources is infallible, and they do not answer the same question.

Use this distinction:

- **Requirement:** what an authorized person says should be true.
- **Repository fact:** what a specific tracked file or Git state currently contains.
- **Observation:** what a command or behavior produced under recorded conditions.
- **Inference:** a conclusion drawn from facts or observations that has not been checked directly.
- **Unknown:** something material that the available evidence does not answer.

For example:

> **Requirement:** cancelled reservations should not appear as available checkouts.
>
> **Repository fact:** `reservations.rs` includes a cancelled status.
>
> **Observation:** the steward page displayed a cancelled reservation in the checkout list using the demo fixture.
>
> **Inference:** the page query may not filter by reservation status.
>
> **Unknown:** whether any other checkout path applies a separate filter.

The inference may be excellent. It is still not a fact until the relevant path is inspected or exercised.

> **Director's question:** What does the current evidence establish, and what am I still assuming?

## Why Vibecoded Software Breaks Here

Imagine receiving this handoff:

> “Waystation is a little Rust website. It keeps reservations in a JSON file and sends confirmation messages directly after each request. Please add a reservation export.”

The description sounds specific enough to act on. An eager agent could find the first JSON-related code, add an export beside it, and demonstrate a plausible file.

Now imagine that the repository actually uses SQLite as its source of truth. The JSON is a demo-data import format. Confirmations are committed as jobs and recorded later by a worker. The export reads only the import fixture, so the demo succeeds with the original sample records and silently omits every new reservation.

The failure has a recognizable shape:

| Part | What happened |
|---|---|
| Convincing happy path | The exported file contains the sample reservations. |
| Hidden assumption | A JSON file that contains reservations must be the live source of truth. |
| Trigger | A user creates a reservation after the fixture was imported. |
| Observable failure | The new reservation is missing from the export. |
| Underlying cause | The change followed the handoff story instead of the actual data path. |

“Use best practices” would not fix this. The missing practice is grounded investigation: identify the source of truth, trace the relevant workflow, and label uncertainty before choosing where to change the system.

## The System Model

Repository investigation is not a tour of every file. Begin at the requested behavior and widen only far enough to find the boundaries that determine it.

```text
Requested behavior
       |
       v
Entry point and callers
       |
       v
Rules and state changes
       |
       v
Persistence and external effects
       |
       v
Checks, configuration, and runtime evidence
```

At each layer, look for ownership and evidence:

| Area | Questions | Useful evidence |
|---|---|---|
| Authority | Which repository instructions and user constraints apply? | Local instruction files, contribution guide, explicit user authorization |
| Git state | Which branch and commit are present? Is the worktree already changed? | `git status`, `git log`, `git diff` |
| Tooling | How is the system built, checked, and started? | Manifests, lockfiles, toolchain files, automation configuration |
| Entry points | Where does the relevant request, command, or event enter? | Routes, command definitions, handlers, public interfaces |
| State and rules | Which values change, and which rules should always hold? | Domain types, validation, service logic, tests |
| Persistence | Which data is authoritative, derived, cached, imported, or generated? | Migrations, storage adapters, fixture loaders, database configuration |
| Effects | What crosses the process boundary? | Worker calls, filesystem writes, network clients, message adapters |
| Evidence | What currently checks or reveals the behavior? | Tests, static checks, logs, health output, safe runtime exercises |

### A useful map format

Ask the agent to report a compact table instead of a stream-of-consciousness tour:

| Claim | Classification | Evidence | Confidence or gap |
|---|---|---|---|
| The application uses SQLite for live reservations | Repository fact | Manifest dependency, migration files, storage call path | High for the inspected path; runtime file location unverified |
| A worker records notification jobs | Repository fact | Worker entry point and notification adapter | High |
| A reservation survives restart | Observation | Create with fixture database, restart, retrieve same identifier | Observed once in the local lab environment |
| All writes use the same storage path | Inference | Two known callers reach the adapter | Other callers have not yet been searched |
| Production uses the same configuration | Unknown | No deployment configuration inspected | Requires environment owner or deployment evidence |

File paths and line numbers are locators, not proof by themselves. Read the cited code or configuration and compare it with the claim.

## Decisions You Own

The agent can gather evidence and propose a boundary. You decide what investigation is sufficient for the risk.

| Decision | Why it matters | Evidence needed |
|---|---|---|
| The exact objective | A vague request can make the agent map the wrong system | Observable behavior, affected user, non-goals |
| The authorized scope | Inspection can cross into private directories, credentials, or external systems | Repository root, applicable instructions, explicit permissions |
| Compatibility that must remain | A locally sensible change can break an unseen caller or stored format | Caller search, public docs, tests, migration and release history |
| The confidence required | A documentation correction and a destructive migration do not need the same depth | Impact, reversibility, failure cost, independent checks |
| Which unknowns can remain | Silent assumptions become accidental design decisions | Named unknowns, consequences, owner acceptance or escalation |

If the agent proposes a consequential choice before the evidence determines it, pause. Ask for alternatives or obtain the missing decision from the responsible person.

## Ground the Agent

The first pass is read-only. Adapt this instruction:

```text
We need to understand how this repository currently handles [behavior].
Do not edit files yet.

First:
1. Read the repository-local instructions that apply to this path.
2. Report the repository root, current branch, commit, and worktree state.
3. Inspect the manifests, entry points, relevant callers, storage or external
   boundaries, configuration, and existing checks for this behavior.
4. Run only safe, read-only or documented diagnostic commands.
5. Return a compact system map.

For every important claim, label it as a requirement, repository fact,
observation, inference, or unknown. Cite the file or command output that
supports it. Name the smallest likely change boundary, behavior that must
remain compatible, and failure cases that would need verification.

Do not install tools, reveal secret values, modify data, contact external
services, or broaden the investigation outside the authorized repository.
```

### The Waystation handoff exercise

When the Waystation baseline is released, begin with the handoff statement from the earlier failure example. Do not tell the agent which parts are inaccurate. Ask it to investigate these claims:

1. Reservations are stored in JSON.
2. The web process sends confirmation messages directly.
3. The application has only one runtime process.
4. The documented test command exercises the full reservation workflow.

Your task is not to contradict the handoff automatically. It is to classify each claim using repository and runtime evidence.

Until the baseline is available, use an authorized repository with at least one manifest, one test path, and one persistence or external-effect boundary. State that substitution in the evidence packet.

## Direct the Change

This chapter's change is a repository map, not an application modification.

```text
Goal:
Create evidence/phase-0/repository-map.md so another person can understand
the current [behavior] without relying on our conversation.

Current system:
Use only facts and observations established during the read-only pass.

Principle to preserve:
Requirements, repository facts, observations, inferences, and unknowns must
remain visibly distinct.

Constraints:
Keep the map scoped to [behavior]. Cite relevant paths and commands. Record
the branch and commit inspected. Redact secrets and private values.

Requested change:
Add the map with the behavior flow, ownership boundaries, source of truth,
external effects, current checks, known risks, and unanswered questions.
Do not change application code, tests, configuration, fixtures, or data.

Required evidence:
Show the final diff. Re-run the safe baseline commands used by the map. Verify
that every material fact has a locator and every unsupported conclusion is
labeled as an inference or unknown.

Do not:
Install dependencies, run destructive commands, contact real services, expose
credentials, or “clean up” unrelated findings.

Before editing, propose the exact file, section outline, evidence sources, and
any claim that still needs clarification.
```

The output is useful only if it can be audited. “The code is well structured” is an opinion. “The reservation route calls this handler, which calls this storage function” is a checkable claim.

## Review the Plan

Before approving the map, ask:

- Does it follow the requested behavior or summarize the entire repository?
- Did the agent inspect repository-local instructions and existing work first?
- Did it find both the obvious entry point and the downstream state or effect?
- Did it search for other callers rather than assume there is only one?
- Does it identify authoritative data separately from fixtures and derived output?
- Are commands safe, relevant, and permitted?
- Does each proposed observation record the environment and input used?
- Are conflicts between documentation, code, tests, and runtime behavior visible?
- Will another person know which questions remain unanswered?

Do not authorize an application fix just because the inspection found one. Preserve it as a finding unless the current objective and authority include repair.

## Build in a Bounded Pass

Have the agent create only `evidence/phase-0/repository-map.md`. The first version should contain:

1. Objective and inspected revision.
2. Applicable repository instructions.
3. Worktree and toolchain state.
4. Relevant behavior flow.
5. State ownership and source of truth.
6. External effects and trust boundaries.
7. Current checks and safe baseline results.
8. Facts that contradict the handoff.
9. Inferences, unknowns, and risks.
10. The smallest likely change boundary—without implementing it.

Require the agent to show the diff and explain any deviation from the one-file scope. A discovered security issue, dirty worktree, or missing tool is evidence to record and possibly escalate, not permission to improvise a broad repair.

## Verify the Result

Do not verify a map merely by asking the same agent whether it is accurate. Follow a sample of important claims to independent evidence.

| Claim | Falsifying check | Expected evidence | What it does not prove |
|---|---|---|---|
| The map describes the inspected revision | Compare its branch/commit/worktree section with fresh Git output | Identifiers and change state agree | That another branch or remote is equivalent |
| The named source of truth is used by the workflow | Trace the entry point to the write path and perform the documented disposable-data smoke case | Code path and resulting durable record agree | That every write path uses it correctly |
| Runtime responsibilities are complete | Compare manifests and entry points, then run the documented local startup | Every started process has an owner in the map | That production deployment has the same topology |
| Current checks cover the claimed behavior | Read the assertions, then perturb a disposable input or run a known rejection case | The check observes the requirement and can fail | That the suite covers all important failures |
| External effects are bounded locally | Inspect adapter selection and perform a fixture notification | Output appears only in the recorded-message sink | That every configuration selects the safe adapter |

Your verification set should include:

- a normal fixture workflow;
- a malformed or rejected request at the mapped boundary;
- a documented startup or worker failure using disposable state;
- the existing regression command without changing its tests;
- one trace across the application, persistence, and recorded-effect boundary.

Record exact commands and relevant results. A successful command proves only what that command exercised in that environment.

## Try to Break It

Challenge the map with a conflicting source.

For Waystation, the handoff says notifications are sent directly. Ask the agent to find the strongest evidence for that claim and the strongest evidence against it. Require more than a documentation quote: inspect entry points, call paths, configuration, and one safe runtime observation.

Record the exercise:

1. **Prediction:** State which model you currently expect and why.
2. **Reproduction:** Trigger a fictional notification using disposable fixture data.
3. **Diagnosis:** Identify which process commits the job and which process records the message.
4. **Repair:** Correct the repository map. Do not change application behavior in this chapter.
5. **Regression:** Add the verified process boundary and evidence command to the map so the same false assumption is less likely to return.

If the evidence remains contradictory, keep the disagreement visible. Do not manufacture certainty to make the document look finished.

## Explain It Back

Without reading the agent's summary aloud, explain:

- where the selected behavior enters the system;
- which component owns its rules;
- where authoritative state changes;
- which external or background effects follow;
- which evidence you observed yourself;
- one inference you have not yet verified;
- one part of the system the map intentionally excludes.

Then ask the agent to challenge your explanation with repository evidence. Correct the explanation only when the evidence supports the correction.

## Apply It to Your Project

Choose one behavior in a project you own or are authorized to inspect. Good candidates include saving a form, importing a file, calling an API, generating a report, or running a background task.

Direct a read-only investigation and produce the same compact map. Compare it with what you believed before inspection:

- Which belief became a repository fact?
- Which belief was contradicted?
- Which belief remains an inference?
- Which new unknown would change a future design decision?

Do not force a code change. If the current design is proportionate and the evidence agrees with the requirement, an accurate map is a complete result.

## Evidence Packet

Preserve:

- the original handoff or request;
- the inspected repository root, branch, commit, and worktree state;
- the read-only grounding instruction;
- the final repository map;
- the sample of citations and observations you independently checked;
- exact safe commands and relevant results;
- contradictions, unknowns, and intentionally excluded areas;
- any finding that requires later repair or specialist review;
- a short reflection describing how your model changed.

Do not include credentials, personal data, private URLs, proprietary source excerpts, environment values, or sensitive logs. Record that evidence exists without copying sensitive content.

## Common Traps

- **The exhaustive tour:** The agent lists every directory and dependency. Redirect it to the requested behavior, its callers, state, effects, and checks.
- **Documentation as runtime truth:** The README is evidence of what someone intended to communicate. Compare it with manifests, implementation, and observation.
- **Unlabeled inference:** Phrases such as “therefore,” “probably,” and “appears to” often hide a leap. Ask what direct check would promote the claim to a fact or observation.
- **Inspection that quietly edits:** Some agents fix small issues while exploring. Require a read-only first pass and inspect Git state before and after it.
- **Command theater:** A long list of green commands can create confidence without exercising the behavior. Connect each command to a specific claim and residual uncertainty.
- **Drive-by cleanup:** Mapping reveals tempting improvements. Record them separately unless they are necessary for the authorized objective.

## When to Stop or Escalate

Stop and request direction when:

- repository-local instructions conflict with the requested action;
- the worktree contains overlapping changes whose ownership is unclear;
- inspection would require credentials, private systems, or access outside the authorized root;
- the relevant behavior depends on generated artifacts with no identified canonical source;
- documentation, stored data, and runtime behavior disagree in a way that could cause destructive work;
- the requested next step involves production data, irreversible migration, security acceptance, or domain policy you do not own;
- the repository cannot reproduce its documented baseline and the cause remains unknown.

The map is complete when another person can trace the scoped behavior, check its important claims, see the unknowns, and decide the next action. It does not need to answer unrelated questions.

## The Takeaway

Begin with the system that exists. A request supplies the desired outcome; repository and runtime evidence constrain the path from here to there.

Direct the agent to inspect in a read-only pass, label claims by evidence type, and map only the boundary relevant to the objective.

The strongest result is not a confident summary. It is a compact model whose important claims another person can try to disprove.

---

| Previous | Current | Next |
|:---|:---:|---:|
| [← Course Overview](../README.md) | **The Repository Is Evidence** | [Phase 0 Outline →](README.md) |
