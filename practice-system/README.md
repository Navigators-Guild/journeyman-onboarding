# The Waystation Practice System

**Status:** design ready for prototype review; implementation not yet present

Waystation is the shared application learners will harden throughout the Journeyman path. It is a small community equipment-lending service: members find equipment and request reservations, stewards check equipment out and back in, and operators keep the service healthy.

The application should look credible on its happy path while containing carefully bounded weaknesses in modeling, architecture, persistence, communication, verification, security, and operations. Those weaknesses are teaching material, not a joke at the learner's expense. Every seeded failure must be safe, reproducible, repairable, and connected to a phase outcome.

## Documents

- [System design](DESIGN.md): domain, boundaries, initial architecture, curriculum failure map, alternatives, and delivery gates
- [Phase 0 outline](../00-from-vibes-to-models/README.md): the first learning boundary applied to Waystation
- [The Repository Is Evidence](../00-from-vibes-to-models/01-the-repository-is-evidence.md): the first authored chapter and repository-map exercise
- [Research basis](../RESEARCH.md): evidence and limitations behind the curriculum design

## Learner Contract

Learners will work from one continuous baseline and improve it in bounded steps. They should not throw Waystation away and request a clean rewrite. Earlier repairs become constraints for later work, just as they do in a maintained production system.

The lab must remain safe to run locally:

- all people, equipment, credentials, and messages are fictional;
- outbound messages use a local recording adapter, never a real provider;
- exercises require no production account or paid service;
- destructive drills use disposable data and a one-command reset;
- intentionally vulnerable behavior is bound to the local exercise environment;
- dependencies with known exploitable vulnerabilities are not seeded deliberately.

## Current Next Step

Build a thin prototype that proves the happy-path workflow, reset mechanism, and deterministic exercise harness before introducing the complete brittle baseline. The implementation stack and prototype gate are specified in [DESIGN.md](DESIGN.md#delivery-plan).

---

[Return to the course overview](../README.md)
