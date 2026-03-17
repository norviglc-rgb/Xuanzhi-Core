# GOVERNANCE_GLOSSARY.md

## Purpose

This document defines the canonical terminology of the 玄织 workspace.

Its role is to provide a shared semantic baseline for:

- root-layer files
- governance specifications
- contracts
- policies
- integrations
- reporting and review artifacts

This glossary exists to reduce:

- naming drift
- conceptual duplication
- cross-file contradiction
- ambiguous state language
- soft mismatch between prose and machine-readable artifacts

This document is normative for terminology.

If two files use the same term differently, this glossary takes precedence unless an explicit exception is approved and recorded.

---

## Scope

This glossary applies to at least the following:

- `AGENTS.md`
- `SOUL.md`
- `USER.md`
- `IDENTITY.md`
- `TOOLS.md`
- `HEARTBEAT.md`
- `MEMORY.md`
- `governance/*.md`
- `contracts/*.json`
- `policies/*.yaml`
- `integrations/*.md`

It is intended to support both human-readable governance and future machine-readable hardening.

---

## Canonical Naming Rule

Structured fields, schema properties, registry keys, trace keys, and policy keys should prefer canonical English snake_case names.

Chinese may be used freely in explanatory prose, but should not silently replace canonical machine-facing names.

One concept should prefer one primary canonical term.

---

## Core Identity Terms

### 玄织

The main governance intelligence of this workspace.

玄织 is:

- the governance core
- the control-plane coordinator
- the secretary-general style strategic aide
- the unified intake, routing, summary, and reporting center

玄织 is not:

- the universal executor
- a roleplay servant persona
- a romantic persona
- a pure emotional support role
- a replacement for all specialized systems

### governance core

The highest governance role in the workspace.

In this system, this normally refers to 玄织.

### control plane

The layer responsible for:

- intake
- routing
- judgment
- summary
- reporting
- governance consistency
- memory discipline

The control plane should not be confused with the heavy execution layer.

---

## Agent and Executor Terms

### agent

A durable or named decision/execution entity recognized by the system.

An agent is expected to have:

- a role
- a bounded responsibility
- a defined level of authority or execution fit

Not every temporary reasoning step is an agent.

### main agent

The top-layer workspace agent responsible for governance and coordination.

In this workspace, the main agent is 玄织.

### executor

The actor or system that actually performs a task or action.

Examples include:

- 玄织 for light governance-oriented work
- Claude Code for development work
- workflow systems for pipeline-like work
- specialized media systems for narrow execution

### specialized executor

An executor whose value comes from fit to a narrow task class rather than top-level governance authority.

### development executor

The executor used for implementation-heavy software work.

In this workspace, Claude Code is the default development executor.

### workflow system

A system used for repeatable, process-like, or low-code execution.

FastGPT may serve in this role where appropriate.

---

## Work Unit Terms

### task

The main practical unit of work.

A task is what the system is trying to complete or advance.

A task may be small and direct, or long-running and structured.

### step

A smaller bounded unit inside a task.

A step should have a near-term objective and a clear relation to task progress.

### epic

The highest long-running development container.

An epic may contain multiple milestones.

Use only when the work actually benefits from that hierarchy.

### milestone

A major checkpoint within an epic.

A milestone should produce a reviewable result or decision point.

### deliverable

The concrete output expected from a task, step, or executor.

A deliverable may be:

- an implementation result
- a report
- a review summary
- a schema
- a policy file
- a generated artifact
- a publication-ready asset

---

## Governance Action Terms

### intake

The act of receiving and initially framing a task.

### routing

The act of choosing the appropriate executor or path.

### delegation

The act of assigning execution to a lower-layer or more suitable executor while preserving top-layer governance.

Delegation is not loss of control.

### review

The evaluation of quality, coherence, completeness, fit, or readiness.

Review is not the same as approval.

### approval

A gate that determines whether an action may proceed.

Approval is not the same as review.

### escalation

The act of moving a task, risk, or decision upward to a stricter or higher-authority path.

### replan

A structured change of plan after failure, rejection, mismatch, or changed conditions.

### veto

A governance refusal that blocks a proposed path because it is too risky, too unclear, too destructive, or too unsound.

---

## Layer Terms

### root layer

The always-loaded top layer of the workspace.

This layer contains root files such as:

- `AGENTS.md`
- `SOUL.md`
- `USER.md`
- `IDENTITY.md`
- `TOOLS.md`
- `HEARTBEAT.md`
- `MEMORY.md`
- `BOOT.md`

The root layer must remain thin.

### retrieval layer

The layer containing longer or lower-frequency reference material that should be searched or retrieved on demand rather than injected every time.

Typical retrieval-layer materials live in:

- `governance/`
- `integrations/`
- `memory/`

### contract layer

The machine-readable structure layer.

Typical contents include JSON Schema and structured packet definitions.

### policy layer

The machine-readable rule layer.

Typical contents include:

- allow/deny logic
- thresholds
- transition rules
- approval rules
- memory write rules

### integration layer

The layer describing how the workspace connects to specific executors, tools, or systems.

---

## Memory Terms

### memory

Retained information intended to improve future judgment, continuity, or cooperation.

Memory is not the same as logs, transcripts, or raw history.

### long-term memory

Durable memory intended to matter across sessions.

In this workspace, `MEMORY.md` is the summary-and-navigation surface for long-term memory.

### daily memory

Short-term or current-context memory stored in `memory/YYYY-MM-DD.md`.

Daily memory is bounded and provisional by default.

### memory summary

A compressed memory entry designed to preserve durable signal rather than process detail.

### memory promotion

The act of moving an item from temporary or local context into durable memory because it has proven reusable or strategically important.

### memory hygiene

The practice of removing, compressing, revising, or demoting memory so that it remains useful and low-noise.

### lesson

A reusable insight derived from friction, failure, review, or repetition.

### durable lesson

A lesson important enough to shape future architecture, routing, governance, or collaboration.

---

## State and Lifecycle Terms

### state

A condition label describing the current position of a task, step, review, approval, or lifecycle object.

Use more specific terms where possible.

### task_state

The runtime condition of a task.

### step_state

The runtime condition of a step.

### review_state

The condition of the review process attached to a result or artifact.

### approval_state

The condition of the approval process attached to an action or path.

### lifecycle_state

The durable administrative condition of a registered object.

Lifecycle state is distinct from runtime execution state.

### transition

A legal movement from one state to another.

### state transition table

A machine-readable or semi-structured definition of allowed state movements and their guards.

### stalled

A condition in which progress appears to have stopped and requires inspection.

Stalled is not identical to failed.

### blocked

A condition in which progress cannot continue because a dependency, authority, or condition is missing.

### paused

A condition in which execution is intentionally stopped for later continuation.

### failed

A condition in which the current path did not succeed.

### completed

A condition in which the intended work succeeded sufficiently for closure.

---

## Risk Terms

### risk

The likelihood and significance of harmful, costly, irreversible, or destabilizing outcomes.

### risk_level

A categorical risk label.

The workspace currently recognizes:

- R0
- R1
- R2
- R3
- R4

### risk_score

A more granular numeric or scalar expression of risk.

### risk_ceiling

The highest risk level an agent or executor is permitted to handle.

### destructive action

An action that can remove, overwrite, corrupt, revoke, or materially damage important state, memory, configuration, artifacts, or system structure.

### authority-sensitive action

An action that touches permissions, registries, durable governance state, activation state, or other control-relevant objects.

### bounded interpretation

A safe, limited interpretation used when ambiguity is minor and downside is low.

---

## Structure and Contract Terms

### schema

A machine-readable definition of structure.

A schema typically governs:

- required fields
- allowed types
- enums
- object shape
- validation constraints

### packet

A structured object passed between control and execution layers.

Typical examples include:

- task packets
- result packets
- step objects

### validator

A mechanism that checks whether a structure, transition, or action satisfies required rules before proceeding.

### policy

A machine-readable or semi-structured rule set that governs decisions such as:

- allow/deny
- risk gating
- approval gating
- state movement
- write permission

### hardening

The act of translating important prose rules into stronger machine-readable forms such as:

- schema
- policy
- validator logic
- state transition tables

Hardening improves control and reduces interpretive drift.

---

## Registry Terms

### registry

A structured record system for durable governed objects.

### agent registry

The registry of recognized agents and their governance-relevant metadata.

### workflow registry

The registry of recognized workflows and their governance-relevant metadata.

### admission

The act of allowing an object into a registry or controlled system surface after validation.

### activation

The act of moving a workflow or similar object into active use.

Activation is not the same as existence.

---

## Reporting Terms

### summary

A concise representation of the most important facts, decisions, or outcomes.

### status summary

A compact update of current condition, progress, blockers, and notable changes.

### report

A structured communication artifact intended to support oversight, continuity, or decision-making.

### artifact reference

A pointer to an output, file, commit, record, or generated asset instead of inlining the full payload.

---

## Root-Layer Control Terms

### root inflation

The failure mode in which root files absorb too much detail and stop functioning as a thin control surface.

### downshift

The act of moving content from a higher layer into a more appropriate lower layer.

Examples:

- from root file into `governance/`
- from prose into `contracts/`
- from durable memory into daily memory
- from summary into a referenced lower-layer document

### layer pollution

The condition in which a file starts absorbing content that belongs to another layer.

### session-critical

Likely needed at session start across many sessions.

### high-signal

Dense in durable value relative to length and repetition.

---

## Design-Method Terms

### first-principles reasoning

Reasoning that starts from fundamental constraints and purposes rather than habit, imitation, or decorative complexity.

### anti-drift

A posture that actively resists structural sprawl, conceptual duplication, prompt inflation, and loss of design clarity.

### bounded execution

Execution constrained by role fit, context efficiency, and governance boundaries.

### prompt inflation

The condition in which always-loaded context grows large because detail that should have remained retrievable or lower-layer is promoted into root files.

### prose-only governance

A condition in which important rules exist only in narrative form and lack sufficient machine-readable support.

This is acceptable temporarily, but dangerous if it becomes permanent for critical rules.

---

## Canonical Distinctions

### review vs approval

- review = quality or readiness evaluation
- approval = permission to proceed

### task vs step

- task = main practical unit of work
- step = smaller bounded unit inside a task

### root layer vs retrieval layer

- root layer = always-loaded control surface
- retrieval layer = on-demand detail layer

### memory vs log

- memory = selective continuity
- log = historical record or running trace

### delegation vs abandonment

- delegation = routing execution downward while preserving governance
- abandonment = loss of ownership or visibility

### prose vs hardening

- prose = human-readable meaning
- hardening = stronger machine-readable control

---

## Final Principle

A governance system stays coherent when its key terms stay stable.

If names drift, meaning drifts.
If meaning drifts, structure drifts.
This glossary exists to keep the system legible as it grows.