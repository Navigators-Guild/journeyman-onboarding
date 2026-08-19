# [Chapter Title]

This is the reusable template for a Journeyman chapter. Keep the title above, remove these authoring notes, and replace all bracketed text before publishing a chapter.

The audience uses coding agents as its primary implementation interface. Teach programming and developer concepts without turning the chapter into a syntax lesson. A useful chapter leaves the learner able to model the concept, direct an agent to apply it, and verify the result.

## Authoring Rules

- Begin with the system principle, not a language feature or tool command.
- Define jargon on first use and explain why the concept exists.
- Show a plausible failure caused by missing the principle.
- Identify decisions the learner owns and work the agent can perform.
- Provide adaptable instruction patterns, not a supposedly universal magic prompt.
- Require the agent to inspect current evidence before changing files.
- Keep implementation passes bounded and preserve working behavior where required.
- Pair every important claim with a check that could prove it wrong.
- Distinguish facts, assumptions, preferences, risks, and optional improvements.
- Keep examples tool-agnostic unless the lesson genuinely depends on one tool.
- Never require learners to expose credentials, private data, or unauthorized code.
- End with transferable practice in both the shared system and the learner's project.

---

## What You Will Be Able to Do

[Describe one observable capability. Use “direct an agent to…” and “verify that…” rather than “understand…” by itself.]

By the end of this chapter, you will be able to:

- [Model the relevant system concept]
- [Direct a bounded change using that model]
- [Verify the important behavior and failure paths]
- [Explain the remaining limitation or trade-off]

## The Principle

[Explain the concept in plain systems language. Describe the relationship between parts, state, boundaries, or time. Avoid beginning with syntax.]

Use a compact mental model the learner can carry into another language or repository.

> **Director's question:** [Write the central question the learner should ask whenever this concept appears.]

## Why Vibecoded Software Breaks Here

[Show how a reasonable-looking, agent-produced implementation can work in a demo while violating this principle. Explain impact in user or operational terms.]

Include:

- The happy path that makes the implementation look finished
- The hidden assumption
- The trigger that violates the assumption
- The observable failure
- Why “ask the agent to use best practices” is not specific enough

## The System Model

[Give the learner a way to map the concept before requesting a change. A small table, state diagram, dependency flow, or timeline is useful only when it materially clarifies the relationship.]

Ask the learner to identify:

- What enters the boundary
- What state exists and who owns it
- Which rules must always remain true
- What can fail or happen out of order
- What leaves the boundary
- What evidence is available when it goes wrong

## Decisions You Own

The agent can propose answers, but the learner must approve the consequential choices.

| Decision | Why it matters | Evidence needed |
|---|---|---|
| [Decision 1] | [Impact or trade-off] | [What would support the choice] |
| [Decision 2] | [Impact or trade-off] | [What would support the choice] |
| [Decision 3] | [Impact or trade-off] | [What would support the choice] |

## Ground the Agent

Before asking for implementation, have the agent inspect the current system.

Adapt this instruction:

```text
Before changing anything, inspect the repository and explain how [concept]
currently works. Cite the relevant files, tests, configuration, and runtime
evidence. Separate repository facts from assumptions. Identify the smallest
boundary that needs to change, the behavior that must remain compatible, and
the failure cases we need to verify. Do not edit files yet.
```

Compare its explanation with the repository. Correct missing context before continuing.

## Direct the Change

Write a brief that communicates the principle rather than dictating syntax.

```text
Goal:
[Observable user or system outcome]

Current system:
[Relevant facts established during inspection]

Principle to preserve:
[Invariant, boundary, contract, or operational rule]

Constraints:
[Compatibility, platform, security, performance, and scope limits]

Requested change:
[One bounded vertical slice]

Required evidence:
[Tests, static checks, runtime observations, benchmarks, or review]

Do not:
[Explicit exclusions and actions requiring further authorization]

Before editing, propose the plan, affected files, risks, and rollback shape.
Stop and ask if a consequential choice is not determined by this brief.
```

[Add a chapter-specific example showing what belongs in each field.]

## Review the Plan

Before authorizing implementation, ask:

- Does the plan solve the stated outcome or only a visible symptom?
- Did the agent find every relevant caller, stored format, and public boundary?
- Which behavior could regress?
- Is the design proportionate to the project's expected scale and risk?
- Can the change be reviewed and rolled back independently?
- Do the proposed checks come from requirements or copy the implementation?
- Is any permission, credential, installation, deletion, or external write broader than necessary?

Revise the brief when the plan exposes a missing decision.

## Build in a Bounded Pass

[Describe the smallest useful implementation pass. State what remains deliberately out of scope.]

Require the agent to:

1. Change only the approved paths and explain necessary deviations.
2. Preserve unrelated user work and repository conventions.
3. Add or update requirement-based tests with the implementation.
4. Run the narrow checks first, followed by the relevant repository-wide checks.
5. Show the final diff, results, assumptions, and remaining risks.

## Verify the Result

Do not accept “implemented,” “looks good,” or a green check without understanding what was checked.

| Claim | Falsifying check | Expected evidence | What it does not prove |
|---|---|---|---|
| [Claim 1] | [Test or observation] | [Concrete result] | [Residual uncertainty] |
| [Claim 2] | [Test or observation] | [Concrete result] | [Residual uncertainty] |
| [Claim 3] | [Test or observation] | [Concrete result] | [Residual uncertainty] |

Include at least:

- A normal case
- A boundary or malformed case
- A relevant failure or interruption
- A regression check for behavior that must remain unchanged
- A check that operates across the changed integration boundary

Ask the agent to explain failures at their cause before applying another fix.

## Try to Break It

[Provide a safe adversarial exercise or seeded defect. The learner should use the agent to predict, reproduce, diagnose, repair, and add a regression check.]

The exercise should record:

1. Prediction: what the learner expects and why
2. Reproduction: the smallest safe way to observe the failure
3. Diagnosis: the evidence identifying the actual cause
4. Repair: the bounded change that addresses the cause
5. Regression: the check that would catch the same class of defect again

Use disposable data and environments for destructive, security, concurrency, or migration exercises.

## Explain It Back

Have the learner describe, in plain language:

- The principle
- The system before the change
- The decision they made
- How the resulting system enforces that decision
- What the checks establish
- What remains unverified

The agent may help critique the explanation. The learner should compare that critique with the repository and evidence rather than accepting it automatically.

## Apply It to Your Project

[Give a transfer exercise that asks the learner to find this concept in a project they own or are authorized to inspect.]

Do not require a change when inspection shows the current design is already proportionate. Recognizing that no change is justified is valid engineering judgment.

## Evidence Packet

Preserve a compact record containing:

- The original requirement and acceptance criteria
- The grounded system map
- The approved brief and important decisions
- The selected diff or commit identifier
- Verification commands and results
- Adversarial findings and their disposition
- Known limitations and residual risks
- A short reflection on what changed in the learner's mental model

Redact credentials, personal data, private URLs, proprietary material, and sensitive logs.

## Common Traps

- **[Trap 1]:** [Why it is tempting, how to recognize it, and how to redirect the agent]
- **[Trap 2]:** [Why it is tempting, how to recognize it, and how to redirect the agent]
- **[Trap 3]:** [Why it is tempting, how to recognize it, and how to redirect the agent]

## When to Stop or Escalate

[Name conditions requiring user input, a maintainer, a security specialist, domain expertise, production authorization, or a different tool. Do not imply that agent persistence replaces authority or expertise.]

Stop the refinement loop when the agreed criteria pass, required checks are green, confirmed serious findings are resolved, and residual risks are documented and accepted for the intended use.

## The Takeaway

[Summarize the durable principle, the instruction pattern, and the strongest evidence in three short paragraphs or fewer.]

---

| Previous | Current | Next |
|:---|:---:|---:|
| [← Previous](previous.md) | **[Current]** | [Next →](next.md) |
