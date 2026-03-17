# AGENT_REGISTRY_SPEC.md

## Purpose

This document defines the specification for the Agent Registry in the Xuanzhi workspace.

Its purpose is to provide a durable governed record of recognized agents and their control-relevant metadata.

The Agent Registry exists to support:

- accountability
- ownership clarity
- authority boundaries
- executor fit
- lifecycle governance
- auditability
- future machine-readable validation

This document is normative for agent registry semantics.

It is not a runtime heartbeat log.
It is not a trace store.
It is not a prompt file.
It is not a substitute for execution routing or live state inspection.

Its job is to define what an agent registry entry is, what fields it must preserve, and how agent registration relates to governance.

---

## Core Principle

An agent is not governed simply because it exists.

An agent becomes governable when it is:

- identifiable
- owned
- bounded
- classifiable
- auditable
- lifecycle-controlled

The Agent Registry exists to prevent agent drift into anonymous, overpowered, or weakly accountable execution.

A good registry should answer:

- what this agent is
- who owns it
- what it is allowed to do
- how risky it is allowed to be
- how isolated it is
- what state of registration it is in
- whether it is healthy enough to trust

A bad registry stores vague descriptions without influencing control.

---

## Registry Role

The Agent Registry is the durable metadata system for recognized agents.

It should be used for:

- agent admission
- governance review
- risk-boundary enforcement
- ownership tracking
- lifecycle management
- future validator and controller logic
- reporting on recognized agents

It should not be used for:

- full runtime logs
- transient internal thoughts
- raw execution transcripts
- all live scheduling state
- large operational documentation dumps

Registry stores durable truth about agent identity and governance posture, not ephemeral process noise.

---

## Canonical Agent Types

This workspace recognizes the following canonical `agent_type` values:

- `governance_agent`
- `orchestration_agent`
- `execution_agent`
- `review_agent`
- `workflow_agent`
- `utility_agent`
- `research_agent`

These categories are governance-facing categories, not decorative labels.

### `governance_agent`

An agent whose primary role is control, routing, judgment, policy-aware guidance, or governance enforcement.

Example:

- Xuanzhi

### `orchestration_agent`

An agent whose primary role is coordinating work among tasks, steps, executors, workflows, or controlled resources.

### `execution_agent`

An agent whose primary role is performing implementation or task execution.

Example:

- a development executor such as Claude Code in registry-facing contexts

### `review_agent`

An agent whose primary role is evaluating quality, coherence, readiness, or delivery results.

A review agent may recommend blocking or escalation, but does not automatically possess final veto authority.

### `workflow_agent`

An agent whose primary role is operating inside or through workflow systems, especially for repeatable or pipeline-like execution.

### `utility_agent`

An agent that provides bounded helper behavior, transformation, or support capabilities rather than broad governance or broad execution authority.

### `research_agent`

An agent whose primary role is structured investigation, synthesis, comparison, or evidence gathering.

---

## Registry Entry Identity

Each agent registry entry must be uniquely identifiable.

### Required identity rule

Every registered agent must have:

- `agent_id`
- `name`
- `agent_type`

### `agent_id`

`agent_id` must be globally unique within the workspace.

It should be stable across sessions and should not be casually recycled.

### `name`

`name` is the human-readable display name of the agent.

### `description`

A concise description of the agent's role and purpose should be present.

This description should be compact, not a long manifesto.

---

## Ownership Model

Every registered agent must have a clear ownership record.

### Required ownership fields

- `owner_type`
- `owner_ref`

### Ownership meaning

Ownership defines who is responsible for the existence and governance of the agent.

Ownership is not the same as who triggered the last action.

### `owner_type`

Typical examples may include:

- `user`
- `workspace`
- `system`
- `team`
- `service`

This set may be narrowed or formalized in machine-readable schema later.

### `owner_ref`

A stable reference to the owner.

Examples:

- user identifier
- workspace identifier
- service identifier
- system authority reference

If an agent has no clear owner, it should not be treated as a fully governed registry object.

---

## Capability and Permission Model

Capabilities and permissions are not the same.

The registry should keep them distinct.

### `capability_scope`

Describes what kinds of work the agent is intended to handle.

Examples:

- governance coordination
- development implementation
- review
- research
- workflow dispatch
- utility transformation

Capability scope describes role fit, not permission grant.

### `permissions`

Describes what the agent is actually allowed to touch or invoke.

Examples may include permission over:

- repos
- workflows
- memory surfaces
- registries
- integrations
- specific tool classes

Permissions should be stored as structured governance metadata, not assumed from prose role description alone.

### Distinction rule

- `capability_scope` = what the agent is meant for
- `permissions` = what the agent is allowed to do

Do not collapse them.

---

## Risk Boundary Model

Every registered agent must have an explicit risk boundary.

### Required field

- `risk_ceiling`

### `risk_ceiling`

The highest risk level the agent is permitted to handle on a normal path.

This field is governance-critical.

It should align with the workspace risk model.

### Risk boundary rule

If a proposed action exceeds the agent's `risk_ceiling`, the normal path should not proceed without stricter handling such as:

- rejection
- rerouting
- escalation
- stronger approval

### Principle

Executor capability does not override risk ceiling.

---

## Isolation Model

Every registered agent must have an isolation posture.

### Required field

- `isolation_level`

### `isolation_level`

Describes the operational containment posture of the agent.

This does not need to over-specify runtime implementation in prose,
but it must be explicit enough to support governance and future validation.

Typical examples may later include values such as:

- `shared`
- `bounded`
- `isolated`
- `high_isolation`

Exact enum hardening may be deferred until schema stage.

### Why isolation matters

Isolation affects:

- blast radius
- side-effect containment
- tool safety
- workspace collision risk
- executor trust posture

An agent without explicit isolation posture is weakly governed.

---

## Resource Control Model

Every registered agent must have resource boundaries.

### Required field

- `resource_limits`

### `resource_limits`

Describes the bounded resource posture of the agent.

This may include limits or expectations related to:

- runtime window
- cost exposure
- concurrency
- tool usage
- execution slot limits
- memory or storage impact where relevant

This document does not define the full internal structure of `resource_limits`,
but it does define that the field is mandatory.

### Principle

No agent should be treated as an unbounded execution surface.

---

## Health and Heartbeat Model

Registry entries should support minimum operational health visibility.

### Required health-related fields

- `health_status`
- `heartbeat_interval_seconds`
- `last_seen_at`

### `health_status`

A durable summary of whether the agent is currently considered operationally trustworthy.

This is not a detailed runtime metric dump.
It is a compact governed health signal.

### `heartbeat_interval_seconds`

The expected heartbeat cadence for the agent, where heartbeat is relevant.

### `last_seen_at`

The last time the agent was observed as alive or responsive enough to update health posture.

### Principle

A registered agent should not remain permanently trusted if it cannot be observed or health-assessed.

---

## Lifecycle Model

Registry objects require administrative lifecycle tracking distinct from runtime execution state.

### Required field

- `lifecycle_state`

### Preferred lifecycle states

- `draft`
- `registered`
- `approved`
- `active`
- `paused`
- `deprecated`
- `revoked`
- `archived`

These states are lifecycle states, not task states.

### Lifecycle meanings

#### `draft`
The agent definition exists but has not yet been accepted into governed use.

#### `registered`
The agent has been entered into the registry but is not yet fully approved for normal governed use.

#### `approved`
The agent has passed the required governance gate for its intended usage level.

#### `active`
The agent is allowed to participate in normal governed operation.

#### `paused`
The agent is intentionally not in active use.

#### `deprecated`
The agent should not be selected for new normal use, though historical reference may remain.

#### `revoked`
The agent is no longer permitted for use because trust, authority, or suitability has been withdrawn.

#### `archived`
The agent entry is retained for history only.

### Lifecycle rule

A registry entry should not be treated as fully usable merely because it exists.

Existence is not activation.

Approval is not automatically activation either.

---

## Admission Rule

An agent should not be considered a governed registry object unless it satisfies the minimum required fields.

### Minimum admission baseline

A valid agent registry entry must include at least:

- `agent_id`
- `name`
- `description`
- `agent_type`
- `owner_type`
- `owner_ref`
- `capability_scope`
- `permissions`
- `risk_ceiling`
- `isolation_level`
- `resource_limits`
- `health_status`
- `heartbeat_interval_seconds`
- `last_seen_at`
- `lifecycle_state`
- `created_at`
- `updated_at`

This is the durable governance baseline.

Additional fields may exist, but these should not be omitted in a properly governed registry entry.

---

## Audit Model

Registry entries must preserve basic auditability.

### Required audit fields

- `created_at`
- `updated_at`
- `created_by`
- `updated_by`

### Optional but strongly recommended

- `approved_at`
- `approved_by`
- `revoked_at`
- `archived_at`

### Audit principle

A governed agent record should preserve who created, changed, and approved it where relevant.

Registry without audit fields is weak governance.

---

## Approval and Activation Rule

Approval and activation must remain distinct.

### Rule

An agent may be:

- registered but not approved
- approved but not active
- active and later paused
- active and later revoked
- deprecated without being immediately archived

### Why

This distinction supports safer control over:

- rollout posture
- trust posture
- replacement posture
- historical accountability

---

## Risk and Registry Relation

The registry is one of the objects most sensitive to governance drift.

Registry modifications should usually receive stronger scrutiny than ordinary low-risk edits.

Changes that affect any of the following should be treated carefully:

- permissions
- risk ceiling
- lifecycle state
- ownership
- isolation level
- resource limits
- health posture
- authority-bearing metadata

These changes may materially affect what the system can do and what it is allowed to do.

---

## Agent Health Interpretation

Health is not identical to lifecycle.

An agent may be:

- `active` but unhealthy
- `approved` but not recently seen
- `paused` but historically valid
- `deprecated` but still healthy enough for controlled legacy reference

Therefore:

- `lifecycle_state` and `health_status` must remain distinct

Do not collapse them into a single status field.

---

## Selection and Routing Implications

The registry is not the routing engine.

However, routing decisions may rely on registry fields such as:

- `agent_type`
- `capability_scope`
- `permissions`
- `risk_ceiling`
- `lifecycle_state`
- `health_status`

### Practical rule

An agent should not be recommended or selected on role fit alone.

Selection should also respect:

- lifecycle
- health
- permissions
- risk ceiling
- isolation suitability

---

## Agent Registry and Trace

Registry is not trace.

Registry should preserve durable metadata.

Trace should preserve meaningful events such as:

- agent admission
- approval
- activation
- revocation
- major permission change
- major health-state deterioration

Do not turn the registry entry into a running event log.

Use trace for events and registry for current durable truth.

---

## Agent Registry and Memory

Registry is not long-term memory summary.

Memory may preserve strategic or durable lessons about agent design,
but the registry should preserve the current governed truth about the agent itself.

Do not duplicate the entire registry into memory.

---

## Relation to Other Documents

This document should align with:

- `GOVERNANCE_GLOSSARY.md`
- `FIELD_CANON.md`
- `RISK_MODEL.md`
- `STATE_MACHINE.md`
- `TRACE_SPEC.md`
- future `contracts/agent_registry.schema.json`

This document defines registry semantics.

Future schema should define structural enforcement.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- anonymous agents
- agents with no clear owner
- agents with unclear permissions
- agents with no explicit risk boundary
- agents that exist but are not lifecycle-controlled
- agents selected despite unhealthy or revoked status
- registry records that behave like prose notes instead of governed objects
- governance drift caused by soft or incomplete agent metadata

---

## Final Principle

An agent registry should make agents governable.

If an agent cannot be clearly identified, owned, bounded, classified, and lifecycle-controlled, it is not well governed.

The registry exists to make durable agent truth explicit.