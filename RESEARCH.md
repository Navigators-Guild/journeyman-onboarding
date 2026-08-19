# Research Basis and Freshness Log

**Last evidence review:** 2026-08-19

**Curriculum status:** researched outline, not yet validated as a completed course

This document records why the Journeyman path is designed the way it is. It is not a claim that every cited result generalizes to every learner, agent, language, or workplace. It separates durable software-engineering knowledge from fast-moving evidence about AI-assisted development.

## Research Question

What should a systems thinker learn in order to direct coding agents responsibly and turn plausible software into software whose important claims are supported by evidence?

The course design follows three constraints:

1. Agents remain available as the implementation interface.
2. Learners must still form usable mental models of programs and systems.
3. Progress must be demonstrated through authentic artifacts and observable system behavior, not confidence, transcript length, or syntax recall.

## How to Read the Evidence

Sources are tagged by the kind of support they provide:

- **Durable foundation:** a mature concept, classic paper, or stable body of practice. Its age is not a defect when the underlying problem has not changed.
- **Current empirical evidence:** a recent experiment, observational study, or benchmark. These can inform course design but often have narrow tasks, short time horizons, or model-specific results.
- **Operational standard:** an official specification or maintained technical reference. It establishes a useful practice or vocabulary, not a causal learning result.
- **Emerging guidance:** a current threat model or practitioner synthesis for a rapidly changing area. It should be reviewed frequently and taught with explicit uncertainty.

The source set favors peer-reviewed research, original research organizations, official standards, and primary project documentation. Vendor research is included when it supplies otherwise unavailable data, but its incentives and scope are noted.

## Findings That Shape the Course

### 1. Producing a result and learning to direct the work are different outcomes

A 2026 randomized study of 52 mostly junior developers found that participants using an AI assistant completed an unfamiliar-library task only modestly faster, while scoring lower on a subsequent mastery quiz. The way people used the assistant mattered: explanation-seeking and conceptual follow-up were associated with better learning than simply requesting finished code. This is a small, short-term, vendor-run study, so the course treats it as a warning rather than a universal effect. It supports prediction, explanation, and reflection checkpoints while keeping the agent available.

Sources: [Anthropic, “How AI assistance impacts the formation of coding skills” (2026)](https://www.anthropic.com/research/AI-assistance-coding-skills); [LeetCoach cognitive-forcing pilot, AAAI 2026](https://ojs.aaai.org/index.php/AAAI/article/view/42121).

**Course consequence:** learners ask the agent to explain a system model, make their own prediction, inspect the change, and reconcile prediction with evidence. Merely obtaining working output cannot pass a phase gate.

### 2. Agent success remains task-dependent, and expertise still matters

Recent coding-agent evidence does not support a simple “agents can do software engineering” or “agents cannot do software engineering” conclusion. METR models capability as a reliability curve across tasks of increasing human-expert duration and warns that its tasks are software-heavy and uneven. Anthropic's observational analysis of roughly 400,000 coding sessions found that people usually supplied planning and oversight while the agent supplied more implementation; domain familiarity was associated with successful recovery. Both findings are sensitive to the selected tools, users, and tasks. The Anthropic study also infers expertise and outcomes with classifiers, so it establishes association rather than causation.

Sources: [METR time-horizon methodology and results](https://metr.org/time-horizons/); [Anthropic, “Agentic coding and persistent returns to expertise” (2026)](https://www.anthropic.com/research/claude-code-expertise); [SWE-Lancer benchmark](https://openai.com/index/swe-lancer/).

**Course consequence:** capability claims are bounded by task, environment, permissions, and evidence. The learner owns domain judgment and risk acceptance even when the agent performs most edits.

### 3. AI amplifies the development system around it

DORA's 2025 industry research frames AI as an amplifier of the surrounding organization rather than an independent cure for delivery problems. The important levers remain clear work, fast feedback, a healthy delivery platform, review, and recovery. This is industry research based on surveys and organizational analysis, not a controlled classroom experiment.

Source: [DORA 2025 report](https://dora.dev/research/2025/dora-report/).

**Course consequence:** the curriculum teaches repository hygiene, tests, continuous integration, observability, and rollback as part of agent use—not as cleanup after generation.

### 4. Passing a narrow test is weaker than being ready to merge or operate

METR's merge-readiness work found that solutions which passed core task tests could still contain lint, formatting, typing, maintainability, or other integration blockers. The exact rates are benchmark-specific, but the gap between “the target test passed” and “the change is fit for its repository” is directly relevant.

Source: [METR, “Towards reconciling slowdown with time horizons” (2025)](https://metr.org/blog/2025-08-12-research-update-towards-reconciling-slowdown-with-time-horizons/).

**Course consequence:** verification proceeds in layers: requirement-specific checks, broader repository checks, diff review, adversarial review, and operational evidence where relevant.

### 5. Reliable software comes from explicit boundaries and enforced invariants

Parnas's information-hiding account of modularity remains a durable explanation for why modules should conceal changeable design decisions rather than merely divide code into arbitrary files. Modern API guidance reinforces static enforcement of valid states where practical and dynamic validation at boundaries where not.

Sources: [Parnas, “On the Criteria To Be Used in Decomposing Systems into Modules” (1972)](https://doi.org/10.1145/361598.361623); [Rust API Guidelines: dependability](https://rust-lang.github.io/api-guidelines/dependability.html); [Rust error handling](https://doc.rust-lang.org/stable/book/ch09-00-error-handling.html).

**Course consequence:** Phases 1 and 2 teach state, types, contracts, error semantics, responsibilities, and dependency direction as system-design tools. Rust is an illustration in the sources, not a required course language.

### 6. Data reliability is about declared guarantees, not database presence

Current PostgreSQL documentation shows that isolation levels permit different concurrency phenomena and may require whole-transaction retries. Database constraints enforce rules regardless of which code path submits the data. SQLite's atomic-commit documentation demonstrates how much machinery sits beneath an apparently simple “save.” These are product references, but the underlying lessons transfer.

Sources: [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html); [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html); [SQLite atomic commit](https://www.sqlite.org/atomiccommit.html); [Jepsen consistency models](https://jepsen.io/consistency/models).

**Course consequence:** learners must identify the source of truth, encode invariants near it, choose a consistency guarantee, test interruption, and rehearse restore—not just ask the agent to add a database.

### 7. Networks turn ordinary operations into time- and duplication-sensitive protocols

Lamport's event-ordering model remains foundational because distributed systems lack a single perfectly shared order. Current production guidance on retries emphasizes timeouts, exponential backoff, jitter, retry limits, and idempotency because an absent response does not reveal whether the remote operation happened.

Sources: [Lamport, “Time, Clocks, and the Ordering of Events in a Distributed System”](https://www.microsoft.com/en-us/research/publication/time-clocks-ordering-events-distributed-system/); [Stripe on idempotency](https://stripe.com/blog/idempotency); [AWS SDK retry behavior](https://docs.aws.amazon.com/sdkref/latest/guide/feature-retry-behavior.html).

**Course consequence:** Phase 4 makes time, ordering, ownership, partial failure, and overload visible in diagrams and failure drills before an agent implements retry or concurrency logic.

### 8. No testing technique establishes correctness by itself

Property-based testing checks general rules over generated inputs; fuzzing searches broad input spaces for crashes or violated assertions; mutation testing changes the implementation to see whether the tests notice. Empirical mutation-testing studies suggest these techniques can reveal weaknesses and influence test improvement, but they remain proxies shaped by the generated properties, inputs, and mutants.

Sources: [Claessen and Hughes, QuickCheck](https://doi.org/10.1145/351240.351266); [The Rust Fuzz Book](https://rust-fuzz.github.io/book/); [Google, “Long Term Effects of Mutation Testing”](https://research.google/pubs/long-term-effects-of-mutation-testing/); [cargo-mutants documentation](https://mutants.rs/).

**Course consequence:** Phase 5 starts with the claim and oracle, then selects a combination of examples, properties, integration checks, fuzzing, mutation, review, and operational observation appropriate to the risk.

### 9. Agentic development enlarges the security boundary

NIST's Secure Software Development Framework supplies stable secure-development practices. Its generative-AI profile extends those practices for AI model producers, system producers, and acquirers. OWASP's current agentic guidance addresses newer risks involving prompts, tools, dependencies, credentials, and autonomous actions. OWASP's agentic material is evolving guidance, not evidence that every listed failure has a measured prevalence.

Sources: [NIST SP 800-218, SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final); [NIST SP 800-218A](https://csrc.nist.gov/pubs/sp/800/218/a/final); [OWASP Secure Coding with AI Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html); [SLSA 1.2](https://slsa.dev/spec/v1.2/).

**Course consequence:** Phase 6 treats the agent, its tools, retrieved text, credentials, build inputs, and release channel as parts of the threat model. Least privilege and human authorization apply to actions, not just application users.

### 10. Observability and recovery are part of correctness after release

OpenTelemetry's current model separates traces, metrics, and logs because each answers different operational questions. Google SRE guidance connects user-centered service objectives with actionable alerts, defined incident roles, and practiced response.

Sources: [OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/); [Google SRE incident management guide](https://sre.google/resources/practices-and-processes/incident-management-guide/); [Google SRE SLO adoption and usage](https://sre.google/resources/practices-and-processes/slo-adoption-and-usage/).

**Course consequence:** deployment is not the end of a chapter. Learners must demonstrate how a failure becomes visible, who decides what to do, and how the system returns to a known state.

### 11. Multiple agents are a coordination design choice, not a maturity badge

A 2026 Nature Machine Intelligence study found that collaboration benefits depended on model capability, task decomposability, and topology; coordination could show diminishing or negative returns. MultiAgentBench likewise reports task-dependent coordination behavior. These are controlled benchmark settings, not a universal measurement of production teams.

Sources: [“Capable language models can outgrow the benefits of collaboration” (2026)](https://www.nature.com/articles/s42256-026-01268-y); [MultiAgentBench, ACL 2025](https://aclanthology.org/2025.acl-long.421/).

**Course consequence:** Phase 7 begins with deciding whether work should be delegated at all. Parallel work requires isolated ownership, explicit interfaces, limited permissions, and an integration owner.

### 12. Assessment should resemble the work and collect more than self-report

A 2024 systematic review associates authentic assessment—realistic tasks with contextual constraints—with problem solving and collaboration, while noting implementation burdens. Reviews of engineering competency measures warn that many instruments lack clear competency definitions or validity evidence. A 2023 meta-analysis across 25 studies found a positive average association between structured reflective interventions and academic achievement, but it was not specific to software engineering or AI agents.

Sources: [Vlachopoulos and Makri, authentic assessment systematic review (2024)](https://doi.org/10.1016/j.stueduc.2024.101425); [Cruz et al., engineering competency measurement review](https://doi.org/10.1080/03043797.2019.1671810); [Zhai et al., reflective interventions meta-analysis](https://doi.org/10.1016/j.tsc.2023.101373).

**Course consequence:** the final phase uses a real repository, a reliability case, observable checks, a failure exercise, and an oral or written defense. Reflection supports learning but cannot substitute for working evidence.

## Phase-to-Evidence Map

| Phase | Primary evidence base | Design use | Important limitation |
|---|---|---|---|
| 0: From Vibes to Models | AI-learning experiment; expertise study; DORA | Grounding, prediction, explanation, evidence ledgers | Agent studies are new, tool-specific, and often short-term |
| 1: Programs | API dependability and error models | Valid states, contracts, explicit recovery | Language documentation illustrates rather than proves pedagogy |
| 2: Codebases | Information hiding; semantic compatibility | Responsibilities, interfaces, change boundaries | Architecture quality remains context-dependent |
| 3: Data | Database constraints, isolation, atomic commit, consistency models | Source of truth, transactions, migration and restore drills | Product behavior differs; learners must inspect their actual store |
| 4: Communication | Event ordering; retry and idempotency guidance | Timelines, bounded retry, duplicate-safe operations, overload | Production guidance is not a universal protocol recipe |
| 5: Safe change | Property, fuzz, mutation, merge-readiness evidence | Match test method to claim; inspect the whole diff | Coverage and mutation scores are proxies, not correctness proofs |
| 6: Operations | SSDF, agentic threat guidance, SLSA, OTel, SRE | Trust boundaries, provenance, telemetry, SLOs, incidents | Agent security taxonomies and threats change quickly |
| 7: Scale | Multi-agent empirical studies and benchmarks | Delegate only decomposable work; design coordination | Benchmark collaboration may not match a real repository or team |
| 8: Reliability | Authentic and competency assessment reviews; reflection meta-analysis | Real project, explicit rubric, multiple evidence forms | The Journeyman rubric itself still requires pilot validation |

## Claims This Research Does Not Support

The course must not claim that:

- agent use always increases or always decreases productivity;
- an agent's benchmark score predicts success on an arbitrary repository;
- asking for an explanation proves that the learner or agent understands the system;
- more agents produce a better result;
- a passing test suite proves correctness, security, or production readiness;
- a tool, language, architecture, or prompt is universally best;
- completing the proposed material currently establishes professional certification or job readiness.

## Freshness Policy

Agent capability, agent security, and multi-agent research should be reviewed at least every six months and before a major course release. Tool examples should be checked against the version used by a chapter. Stable foundations should be replaced only when stronger evidence changes the principle, not merely because a newer article exists.

Every research update should record:

- the review date;
- the claim affected;
- whether the source is empirical evidence, a standard, or guidance;
- the population, task, environment, and model studied;
- limitations or conflicts with other evidence;
- the resulting curriculum change, if any.

## Open Validation Work

Before presenting the path as a validated course, the project should:

1. Pilot each phase with members of the intended audience.
2. Measure transfer on an unfamiliar repository, not just the guided practice system.
3. Compare unaided baseline decisions with later agent-directed decisions without forbidding agent use.
4. Use at least two raters for a sample of capstone reliability cases and revise ambiguous rubric language.
5. Track false confidence, unnecessary complexity, unsafe authorization, and failure recovery—not only task completion.
6. Publish anonymized aggregate results, course changes, and null or negative findings.

---

[Return to the course overview](README.md)
