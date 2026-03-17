# CONTROLLER_API_SPEC.md

## Purpose

This document defines the high-level controller action surface of the Xuanzhi workspace.

Its purpose is to provide a stable control-plane API baseline for:

- task intake and routing
- development delegation
- workflow invocation
- governance actions
- memory actions
- GitLab-related actions
- alerting actions
- dangerous-action gating
- future controller implementation

This document is normative for controller action semantics.

It is not a transport protocol specification.
It is not a REST or RPC manual.
It is not a scheduler implementation.
It is not a tool SDK reference.

Its job is to define what categories of controller actions exist, what they mean, and what governance expectations apply to them.

---

## Core Principle

The controller should expose a small set of high-value actions, not an unbounded sea of low-level commands.

A good controller API should make it clear:

- what action is being requested
- why the action belongs to the control plane
- what the expected input shape is
- what output shape or effect is expected
- what risk or approval posture may apply

A bad controller API becomes either:

- too low-level and leaks implementation everywhere
or
- too vague and useless for real control

This workspace prefers high-level, governance-aware actions.

---

## Controller Role

The controller is the execution bridge between Xuanzhi's governance reasoning and the systems that actually perform work.

The controller is expected to:

- normalize incoming actions
- route execution to the correct underlying system
- enforce policy or validator checks where applicable
- preserve trace and reporting signal
- return bounded structured outputs

The controller is not the top governance authority.

Xuanzhi remains responsible for:

- task framing
- routing intent
- approval posture
- escalation posture
- summary and reporting interpretation

---

## Canonical Action Families

The controller should expose actions in the following high-level families:

- `knowledge`
- `workflow`
- `development`
- `governance`
- `memory`
- `gitlab`
- `alerts`
- `dangerous`

These families should stay small and semantically stable.

They are action families, not implementation modules.

---

## Action Envelope

Every controller action should conceptually include:

- `action_family`
- `action_name`
- `args`
- `reasoning_summary`
- `risk_level` where applicable
- `approval_mode` where applicable
- `trace_context` where applicable

This document does not force one exact wire format,
but these concepts should be preserved.

### Principle

Controller actions should be:

- explicit
- bounded
- auditable
- policy-aware

---

## `knowledge` Actions

`knowledge` actions are used for retrieval, lookup, ingest support, or knowledge-surface operations.

Typical examples:

- retrieve relevant project documents
- search memory or knowledge surfaces
- locate supporting evidence
- register or stage knowledge ingest operations

### Typical use cases

- answering grounded questions
- building context for planning
- supporting governance review
- supporting development framing

### Expected controller behavior

The controller should:

- select the appropriate retrieval source or gateway
- return bounded structured results
- avoid forcing large raw content upward unless required
- preserve artifact references where useful

### Not included

`knowledge` actions are not full memory mutation by default.
Durable memory changes belong to `memory` actions.

---

## `workflow` Actions

`workflow` actions are used to invoke, inspect, or coordinate workflow-like execution surfaces.

Typical examples:

- run a workflow
- schedule a workflow
- inspect workflow availability
- check workflow health
- query workflow registry-backed metadata
- request workflow activation-related preparation

### Expected controller behavior

The controller should:

- respect workflow registry truth
- respect approval and activation posture
- preserve traceable workflow invocation summaries
- avoid treating all workflows as always-active or always-safe

### Principle

Workflow invocation is a governed action surface, not just a convenience call.

---

## `development` Actions

`development` actions are used for development delegation and repo-centered implementation control.

Typical examples:

- create development task packet
- dispatch work to Claude Code
- request bounded repo analysis
- collect development result packet
- request checkpoint summary
- prepare delivery-ready review context

### Expected controller behavior

The controller should:

- preserve Xuanzhi -> executor packet semantics
- enforce relevant policy gates
- support bounded execution visibility
- keep result outputs structured and reviewable

### Principle

The controller should not micromanage development keystrokes.

It should manage governed development handoff and return surfaces.

---

## `governance` Actions

`governance` actions are used for policy, registry, approval, review, and other control-plane operations.

Typical examples:

- submit approval request
- record approval decision
- register an agent
- register a workflow
- update governed lifecycle state
- request governance review
- create or update policy-aware records

### Expected controller behavior

The controller should:

- validate governance-sensitive structures
- respect admission rules
- distinguish review from approval
- preserve audit signal
- enforce lifecycle and registry constraints

### Principle

The governance action family exists to make durable controlled changes explicit.

---

## `memory` Actions

`memory` actions are used for memory-aware writes, revisions, promotions, or lookups that alter memory state.

Typical examples:

- append daily memory note
- update long-term memory summary
- promote a lesson
- revise durable memory entry
- remove or archive a memory item where policy permits

### Expected controller behavior

The controller should:

- respect memory write policy
- distinguish long-term memory from daily memory
- preserve trace signal for meaningful durable memory changes
- reject or escalate destructive memory actions when risk requires it

### Principle

Memory mutation is governance-relevant because it changes future behavior.

---

## `gitlab` Actions

`gitlab` actions are used for repo-centered control operations through GitLab CE.

Typical examples:

- create repository
- create issue
- create branch context
- create or inspect merge request
- inspect pipeline status
- gather repo change metadata

### Expected controller behavior

The controller should:

- respect repo template and governance posture
- prefer issue-linked and branch-aware workflows
- preserve merge and CI gate awareness
- return structured status rather than giant raw payloads

### Principle

GitLab actions should support governed development flow, not bypass it.

---

## `alerts` Actions

`alerts` actions are used to create, route, summarize, or acknowledge abnormal or attention-worthy conditions.

Typical examples:

- raise stalled task alert
- emit high-risk block alert
- record escalation alert
- summarize unresolved warnings
- acknowledge alert handling

### Expected controller behavior

The controller should:

- preserve severity
- preserve affected object linkage
- preserve summary and next control point
- avoid alert spam by default

### Principle

Alerting should increase legibility, not create noise.

---

## `dangerous` Actions

`dangerous` actions are a special high-scrutiny family for actions that may be destructive, overreaching, or deeply sensitive.

Typical examples:

- destructive delete
- registry revocation
- major permission expansion
- sensitive infra change
- runtime-critical control mutation

### Expected controller behavior

The controller should:

- require stronger validation
- consult risk posture
- consult approval posture
- stop or escalate when required
- preserve high-quality trace and reporting

### Principle

Dangerous actions should never feel normal merely because the controller can technically express them.

---

## Input Expectations

Controller actions should prefer bounded structured arguments.

Typical expectations include:

- canonical identifiers where applicable
- references instead of giant embedded payloads
- summary-level reasoning rather than full process dumps
- explicit action targets
- explicit action purpose when ambiguity matters

### Principle

Controller inputs should support validation and policy checks.

They should not depend on informal interpretation of giant raw blobs whenever avoidable.

---

## Output Expectations

Controller outputs should be structured and bounded.

Typical outputs should include some combination of:

- `summary`
- `status_summary`
- `artifact_refs`
- `task_state`
- `review_state`
- `approval_state`
- `risk_level`
- `next_step`
- `trace_id`

### Principle

The controller should return enough to support review, routing, and reporting,
without forcing the top layer to parse raw system noise every time.

---

## Controller and Trace

Meaningful controller actions should support trace generation.

At minimum, trace should exist for:

- durable governance mutations
- agent/workflow admission events
- approval outcomes
- high-risk action handling
- meaningful development delegation
- major memory changes
- alerts and escalations

The controller is a major bridge for trace creation,
but it should prefer structured trace events rather than narrative logs.

---

## Controller and Policy

The controller should be policy-aware.

Where machine-readable policy exists, the controller should be able to consult or enforce it.

Examples include:

- `state_transitions.yaml`
- `risk_policy.yaml`

### Principle

The controller should not behave as if policy documents are decorative attachments.

If policy exists, controller design should leave room to honor it.

---

## Controller and Validation

The controller should validate:

- packet shape where contracts exist
- registry admission baseline where schemas exist
- approval and lifecycle constraints where rules exist
- dangerous-action prerequisites where policy requires it

This does not mean every action must be slowed down by maximum validation,
but meaningful governed actions should not skip structural checks.

---

## Dangerous-Action Gate

Dangerous actions should not share the same trust posture as ordinary actions.

A dangerous-action gate should exist conceptually for actions that are:

- destructive
- highly sensitive
- authority-expanding
- hard to reverse
- registry- or activation-critical
- infra-critical

### Dangerous-action gate should support

- stronger risk check
- stronger approval check
- escalation path
- strong-reporting mode
- high-quality trace

---

## Controller and Approval

The controller is not the source of approval legitimacy.
It is the execution bridge for approval-aware actions.

The controller should be able to support actions such as:

- request approval
- record approval outcome
- block action due to missing approval
- escalate when approval cannot be resolved autonomously

### Principle

Controller support for approval must preserve the distinction between:

- review
- approval
- veto
- escalation

---

## Controller and Registry

The controller should support registry-aware actions without turning the registry into a runtime dump.

Typical registry-related actions may include:

- admit entry
- validate entry
- update lifecycle state
- update health status
- revoke entry
- archive entry

### Principle

Registry mutations are governance-significant and should remain explicit.

---

## Controller and Scheduler Boundary

The controller may later interact with a scheduler,
but this document does not define the scheduler.

The controller action surface should remain scheduler-compatible,
but it should not be forced to encode full scheduling logic at this stage.

### Principle

Keep the controller API high-level.
Do not prematurely collapse scheduler design into controller actions.

---

## Implementation Guidance

A future implementation may map these high-level action families to:

- internal methods
- service handlers
- RPC endpoints
- workflow dispatch adapters
- policy validators
- external integrations

This mapping is intentionally deferred.

What matters now is preserving the semantic surface.

---

## Relation to Other Documents

This document should align with:

- `STATE_MACHINE.md`
- `RISK_MODEL.md`
- `TRACE_SPEC.md`
- `DEV_TASK_MODEL.md`
- `APPROVAL_POLICY.md`
- `AGENT_REGISTRY_SPEC.md`
- `WORKFLOW_REGISTRY_SPEC.md`
- `CLAUDE_CODE_EXECUTION_SPEC.md`
- `GITLAB_INTEGRATION.md`

This document defines controller action semantics.

It does not replace packet schemas, policy files, or integration-specific execution specs.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- controller actions that are too low-level to govern
- controller actions that are too vague to validate
- dangerous mutations hiding inside ordinary action surfaces
- policy existing but not being structurally usable
- integration sprawl without a common control surface
- top-layer reasoning having no stable action vocabulary

---

## Final Principle

A good controller API gives the control plane a small number of powerful, governable actions.

It should make work easier to route, easier to validate, easier to trace, and harder to let drift silently.

That is the point.