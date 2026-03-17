# WORKFLOW_REGISTRY_SPEC.md

## Purpose

This document defines the specification for the Workflow Registry in the Xuanzhi workspace.

Its purpose is to provide a durable governed record of recognized workflows and their control-relevant metadata.

The Workflow Registry exists to support:

- workflow accountability
- ownership clarity
- activation control
- permission visibility
- risk-aware governance
- lifecycle management
- auditability
- future machine-readable validation

This document is normative for workflow registry semantics.

It is not a runtime execution log.
It is not a full workflow definition store.
It is not a substitute for execution trace or scheduler state.

Its job is to define what a workflow registry entry is, what fields it must preserve, and how workflow registration relates to governance.

---

## Core Principle

A workflow is not governed merely because it exists somewhere in a tool, directory, or workflow system.

A workflow becomes governable when it is:

- identifiable
- owned
- classifiable
- risk-declared
- permission-aware
- lifecycle-controlled
- health-visible

The Workflow Registry exists to prevent workflows from drifting into:

- anonymous automation
- unreviewed activation
- unclear permissions
- hidden risk
- silent operational sprawl

A good workflow registry should answer:

- what this workflow is
- who owns it
- what class of workflow it is
- what triggers it
- what permissions it depends on
- what its risk posture is
- whether it is approved
- whether it is active
- whether it is healthy enough to trust

A bad registry stores descriptions without influencing activation or governance.

---

## Registry Role

The Workflow Registry is the durable metadata system for recognized workflows.

It should be used for:

- workflow admission
- workflow approval
- workflow activation control
- lifecycle management
- governance review
- reporting on recognized workflows
- future validator and controller logic

It should not be used for:

- every runtime event
- every historical execution record
- long workflow implementation manuals
- raw trace logs
- copied workflow source payloads

Registry stores durable governed truth about workflows, not all execution detail.

---

## Canonical Workflow Types

This workspace recognizes the following canonical `workflow_type` values:

- `automation_workflow`
- `scheduled_workflow`
- `agent_tool_workflow`
- `data_pipeline_workflow`
- `maintenance_workflow`
- `governance_workflow`

These categories are governance-facing categories, not decorative labels.

### `automation_workflow`

A workflow that automates a bounded repeatable process.

### `scheduled_workflow`

A workflow that is intended to run on a schedule or recurring cadence.

### `agent_tool_workflow`

A workflow that exists mainly as a tool-facing or agent-invoked execution path.

### `data_pipeline_workflow`

A workflow focused on ingestion, transformation, transfer, or processing of data-like assets.

### `maintenance_workflow`

A workflow used to maintain systems, indexes, state, or operational surfaces.

### `governance_workflow`

A workflow whose primary purpose is review, reporting, approval support, governance checks, or similar control-plane functions.

---

## Registry Entry Identity

Each workflow registry entry must be uniquely identifiable.

### Required identity rule

Every registered workflow must have:

- `workflow_id`
- `name`
- `workflow_type`

### `workflow_id`

`workflow_id` must be globally unique within the workspace.

It should be stable and should not be casually recycled.

### `name`

`name` is the human-readable display name of the workflow.

### `description`

A concise description of the workflow's purpose should be present.

This description should remain compact and governance-relevant.

---

## Ownership Model

Every registered workflow must have a clear ownership record.

### Required ownership fields

- `owner_type`
- `owner_ref`

### Ownership meaning

Ownership defines who is responsible for the workflow's existence, use, and governance posture.

Ownership is not the same as who last triggered it.

### `owner_type`

Typical examples may include:

- `user`
- `workspace`
- `system`
- `team`
- `service`

This set may be hardened later in schema.

### `owner_ref`

A stable reference to the owner.

If a workflow has no clear owner, it should not be treated as a fully governed workflow registry object.

---

## Trigger Model

Every registered workflow should declare how it may be started.

### Required field

- `trigger_types`

### `trigger_types`

A list of workflow trigger categories.

Typical examples may include:

- manual
- schedule
- event
- api
- agent
- webhook

This document does not freeze the full enum yet,
but it does require that trigger posture be explicit.

### Principle

A workflow with hidden or unclear trigger surfaces is weakly governed.

---

## Permission Model

Every registered workflow must declare permission posture.

### Required field

- `permissions`

### `permissions`

Describes what the workflow is allowed to touch or invoke.

Examples may include permissions related to:

- repos
- workflows
- memory surfaces
- integrations
- registries
- external APIs
- publishing endpoints
- media systems

The exact internal structure may evolve,
but the presence of a structured permissions field is mandatory.

A workflow should not be treated as governed if its effective access surface is unclear.

---

## Resource Control Model

Every registered workflow must declare resource posture.

### Required field

- `resource_limits`

### `resource_limits`

Describes bounded resource expectations or limits, potentially including:

- runtime window
- concurrency
- budget
- execution slot pressure
- external service usage
- storage or artifact volume concerns where relevant

This document does not fully define the internal object shape,
but it requires that workflow resource posture be explicit.

---

## Risk Model

Every registered workflow must declare risk posture.

### Required field

- `risk_level`

### Optional but useful

- `risk_summary`

### `risk_level`

The categorical risk class of the workflow under normal expected use.

This should align with the workspace risk model.

### Principle

Workflows are not low-risk merely because they are repeatable.

A repeatable high-risk workflow is still high-risk.

Workflow risk should consider:

- destructiveness
- target sensitivity
- authority implications
- blast radius
- recoverability
- downstream automation consequences

---

## Approval Model

Approval and activation must remain distinct.

### Required field

- `approved`

### Optional but strongly recommended

- `approved_at`
- `approved_by`

### `approved`

A boolean or equivalent lifecycle fact indicating whether the workflow has passed the required governance gate for normal use.

### Approval rule

Approved status does not automatically imply active status.

Approval means the workflow is allowed to exist as a trusted governed candidate for use under its declared posture.

---

## Activation Rule

### Core rule

A workflow must be approved before it may be active.

This is a fundamental governance rule.

### Activation implication

A workflow may be:

- registered but not approved
- approved but not active
- active and later paused
- active and later deprecated
- active and later revoked

Approval and activation must not be collapsed.

---

## Lifecycle Model

Workflow registry entries require administrative lifecycle tracking distinct from runtime execution state.

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

These are lifecycle states, not runtime execution states.

### Lifecycle meanings

#### `draft`
The workflow definition exists conceptually or locally but is not yet admitted into governed use.

#### `registered`
The workflow has been entered into the registry but has not yet passed full governance gating.

#### `approved`
The workflow has passed the required governance approval posture.

#### `active`
The workflow is permitted for normal governed use.

#### `paused`
The workflow is intentionally inactive for now.

#### `deprecated`
The workflow should not be selected for new normal use, though historical reference remains.

#### `revoked`
The workflow is no longer permitted for use.

#### `archived`
The workflow entry is retained for history only.

### Lifecycle distinction rule

Do not confuse:

- `lifecycle_state`
with
- runtime run status

A workflow may be active in lifecycle terms while not currently running.

---

## Version and Definition Linkage

Every registered workflow should preserve version awareness and linkage to its actual definition.

### Required field

- `version`

### Strongly recommended field

- `definition_ref`

### `version`

The declared version of the workflow entry or its governed definition.

### `definition_ref`

A pointer to the actual workflow definition, source file, system entry, or authoritative implementation location.

The registry should point to the definition.
It should not absorb the full definition payload unless the workflow is extremely small.

---

## Health Model

Workflow registry entries should support minimum health visibility.

### Required field

- `health_status`

### Strongly recommended

- `last_checked_at`

### `health_status`

A durable summary of whether the workflow is currently considered operationally trustworthy.

This is not a detailed execution log.
It is a governance-facing health signal.

### Why health matters

A workflow may be:

- approved but unhealthy
- active but repeatedly failing
- lifecycle-valid but integration-broken

Lifecycle and health must remain distinct.

---

## Admission Rule

A workflow should not be treated as a governed registry object unless it satisfies the minimum required fields.

### Minimum admission baseline

A valid workflow registry entry must include at least:

- `workflow_id`
- `name`
- `description`
- `workflow_type`
- `owner_type`
- `owner_ref`
- `trigger_types`
- `permissions`
- `resource_limits`
- `risk_level`
- `approved`
- `version`
- `health_status`
- `lifecycle_state`
- `created_at`
- `updated_at`

This is the durable governance baseline.

Additional fields may exist,
but these should not be omitted in a properly governed workflow registry entry.

---

## Audit Model

Registry entries must preserve basic auditability.

### Required audit fields

- `created_at`
- `updated_at`
- `created_by`
- `updated_by`

### Strongly recommended

- `approved_at`
- `approved_by`
- `revoked_at`
- `archived_at`
- `last_checked_at`

### Audit principle

A governed workflow record should preserve who created, changed, approved, or revoked it where relevant.

Registry without audit fields is weak governance.

---

## Trigger and Activation Implications

Trigger declaration affects governance posture.

A workflow with:

- broad triggers
- external triggers
- automatic recurring triggers
- trigger surfaces touching sensitive systems

may deserve stronger scrutiny than a manually triggered bounded workflow.

### Practical rule

Do not assess workflow governance only from the workflow body.

Also assess:

- trigger exposure
- permission exposure
- activation posture
- risk level
- health
- lifecycle

---

## Health and Lifecycle Distinction

A workflow may be:

- `active` but unhealthy
- `approved` but not active
- `paused` but otherwise healthy
- `deprecated` but still historically valid

Therefore:

- `health_status` and `lifecycle_state` must remain distinct

Do not collapse them into a single generic status field.

---

## Workflow Registry and Trace

Registry is not trace.

Registry should preserve current durable truth.

Trace should preserve meaningful events such as:

- workflow admission
- approval granted
- activation
- pause
- deprecation
- revocation
- major permission change
- major health deterioration

Do not turn the registry entry into a running event log.

Use trace for events and registry for durable governed state.

---

## Workflow Registry and Memory

Registry is not long-term memory summary.

Memory may preserve strategic notes or lessons about workflow design,
but the registry should preserve the current governed truth about the workflow itself.

Do not duplicate the registry into memory.

---

## Workflow Selection and Routing Implications

The registry is not the scheduler or router,
but scheduling and routing decisions may rely on registry fields such as:

- `workflow_type`
- `trigger_types`
- `permissions`
- `risk_level`
- `approved`
- `health_status`
- `lifecycle_state`

A workflow should not be selected merely because it exists.

Selection should also respect:

- approval
- lifecycle
- health
- permissions
- risk posture
- trigger suitability

---

## Relation to Other Documents

This document should align with:

- `GOVERNANCE_GLOSSARY.md`
- `FIELD_CANON.md`
- `RISK_MODEL.md`
- `STATE_MACHINE.md`
- `TRACE_SPEC.md`
- future `contracts/workflow_registry.schema.json`

This document defines workflow registry semantics.

Future schema should define structural enforcement.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- anonymous workflows
- workflows with no clear owner
- workflows with unclear permissions
- workflows activated before approval
- repeatable high-risk automation treated as harmless
- workflow entries with no health visibility
- registry entries that act like prose notes instead of governed objects
- automation sprawl without lifecycle control

---

## Final Principle

A workflow registry should make workflows governable.

If a workflow cannot be clearly identified, owned, permissioned, risk-declared, approved, and lifecycle-controlled, it is not well governed.

The registry exists to make durable workflow truth explicit.