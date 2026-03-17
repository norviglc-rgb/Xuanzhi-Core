# APPROVAL_POLICY.md

## Purpose

This document defines the approval policy of the Xuanzhi workspace.

Its purpose is to provide a stable approval baseline for:

- whether an action may proceed
- which approval path applies
- how approval differs from review
- when governance-level approval is sufficient
- when human approval is required
- how approval interacts with risk, workflow activation, and long-running development

This document is normative for approval semantics.

It is not a full scheduler implementation.
It is not a substitute for risk classification.
It is not a review handbook.
It is not a runtime trace log.

Its job is to define who or what must approve which kinds of actions, and what approval outcomes mean for the next control step.

---

## Core Principle

Approval is permission, not praise.

A useful approval policy should answer:

- does this path have permission to proceed
- what level of authority is required
- is governance approval enough
- is human intervention required
- what happens after approval is granted or denied

A bad approval policy confuses approval with review, or allows approval to become invisible, inconsistent, or decorative.

Therefore this workspace treats approval as a bounded control gate.

---

## Approval Is Not Review

Approval and review must remain distinct.

### Review

Review asks questions such as:

- is the output coherent
- is the result good enough
- did the work meet the intended objective
- are there major blockers or findings

### Approval

Approval asks questions such as:

- may this action proceed
- does the current authority path allow it
- is the risk posture acceptable
- does this require stricter governance or human involvement

### Distinction rule

A result may:

- pass review but still fail approval
- fail review without ever needing approval
- require approval before execution
- require review after execution

Do not collapse review and approval into one generic gate.

---

## Approval Modes

This workspace recognizes the following approval modes:

- `not_required`
- `governance_required`
- `human_required`

These modes are control-plane categories, not decorative labels.

### `not_required`

No explicit approval gate is required for the current action under current posture.

### `governance_required`

Approval is required, but it may be resolved inside the governed system path.

This typically means Xuanzhi or an equivalent governance-capable approval path may decide.

### `human_required`

The action may not proceed on the normal autonomous path.

Human authorization is required before continuation.

---

## Approval Authority Levels

Approval authority should be thought of in bounded layers.

### Layer 1: No explicit approval

For low-risk, non-destructive, low-authority, reversible actions.

### Layer 2: Governance approval

For actions that are significant enough to require a permission gate, but still resolvable within the Xuanzhi governance path.

### Layer 3: Human approval

For actions that exceed autonomous trust boundaries, touch severe risk, or require explicit human authorization.

---

## Default Approval Posture by Risk Level

These are default tendencies, not a substitute for specific policy.

### `R0`

Default approval mode:

- `not_required`

Typical posture:

- proceed normally
- lightweight execution or analysis
- no separate approval path needed

### `R1`

Default approval mode:

- `not_required`

Typical posture:

- reversible low-risk work
- may proceed without separate approval unless another sensitivity rule applies

### `R2`

Default approval mode:

- `governance_required` only when sensitivity, authority, or durability justifies it
- otherwise `not_required`

Typical posture:

- moderate changes may still proceed without explicit approval if clearly bounded
- but durable, sensitive, or structural effects often justify governance approval

### `R3`

Default approval mode:

- `governance_required`
- `human_required` when uncertainty, authority, or destructive consequences are too high for autonomous governance resolution

Typical posture:

- stronger gate
- stronger review of authority and justification
- stricter continuation conditions

### `R4`

Default approval mode:

- not a normal approval path
- immediate block and escalation
- typically `human_required` for any continuation decision

`R4` is a stop class, not a routine “please approve this” class.

---

## Actions That Commonly Require Governance Approval

Governance approval is commonly appropriate for actions such as:

- activating a workflow
- changing durable governance behavior
- changing important memory in a durable way
- modifying agent or workflow registry entries
- performing structurally meaningful project changes
- significant development actions with notable but bounded downside
- authority-sensitive but not clearly overreaching actions
- moderate-to-high-impact changes that remain inside normal trust boundaries

### Principle

Governance approval should be used when the action is too significant for silent normal execution, but not so extreme that autonomy must stop entirely.

---

## Actions That Commonly Require Human Approval

Human approval is commonly appropriate for actions such as:

- clearly high-risk destructive actions
- actions near or beyond autonomous authority boundaries
- severe runtime or infra changes with meaningful downside
- actions with major business, safety, or governance implications
- unresolved `R3` actions with weak information
- any `R4` continuation path
- major permission expansion
- major sub-agent authority expansion
- sensitive deletion or revocation where autonomous trust is not enough

### Principle

Human approval is required when the cost of autonomous permission error is too high.

---

## Approval and Sensitive Objects

Sensitive objects increase the chance that approval is required.

Examples of sensitive object classes include:

- memory
- knowledge
- configuration
- CI/CD
- nginx or gateway/runtime routing
- docker runtime
- registries
- workflow activation surfaces
- permission-bearing objects
- sub-agent authority surfaces

Touching a sensitive object does not automatically imply `human_required`,
but it should raise scrutiny and often pushes the action toward `governance_required` or stronger.

---

## Approval and Workflow Activation

Workflow activation is a special approval case.

### Core rule

A workflow must be approved before it may be active.

This rule should align with the workflow registry model.

### Practical meaning

A workflow may exist in the registry without being active.

Approval is the control gate that allows activation to become possible.

Activation should not silently happen merely because a definition exists or a trigger exists.

---

## Approval and Long-Running Development

Long-running development may encounter approval at multiple levels.

### Common approval moments

- before a risky structural change
- before a milestone continuation path
- before merge or release-like gates
- after review if the next path has elevated risk
- after a replan when the new path materially changes the original risk or scope

### Principle

Do not force approval at every tiny step.

Approval should appear at meaningful control points,
not as ceremony noise.

---

## Approval Outcomes

The canonical approval outcomes are:

- `approval_not_required`
- `approval_pending`
- `approval_running`
- `approval_granted`
- `approval_rejected`
- `approval_escalated`

These meanings should align with the state machine.

### `approval_not_required`

No approval gate applies.

### `approval_pending`

Approval is required but not yet started.

### `approval_running`

Approval evaluation is actively in progress.

### `approval_granted`

Permission to proceed has been granted.

### `approval_rejected`

Permission to proceed has been denied.

The default next action is usually:

- replan
- or stop, depending on context

### `approval_escalated`

Approval cannot be resolved on the current path and has been escalated.

---

## What Happens After Approval Decisions

### After `approval_granted`

The action may proceed on the approved path, subject to:

- continued risk posture
- state validity
- review gates where relevant

Approval does not erase the need for later review.

### After `approval_rejected`

The default next action is not blind repetition.

The default next action is usually:

- `replanning`
- or `cancelled`
- or `escalating` if the conflict cannot be responsibly resolved

### After `approval_escalated`

The system should not proceed on the current normal path.

A stricter authority path must resolve the next step.

---

## Approval Trigger Heuristics

Approval should be considered when one or more of the following are true:

- risk is meaningfully elevated
- the target is sensitive
- the change is hard to reverse
- the blast radius is broad
- the authority implication is unclear
- the action changes durable governance state
- the action changes activation posture
- the action changes permissions or registry truth
- the action has high cost with real downside
- the executor is capable but the trust boundary is still insufficient

These are heuristics, not the final machine-readable rule engine.
They exist to guide governance posture and later policy hardening.

---

## Human Escalation Triggers

Human approval should be strongly considered or required when:

- the action is `R4`
- the action is clearly unauthorized or overreaching
- the action is clearly destructive and poorly justified
- the action is high-cost with weak information
- governance approval cannot confidently resolve the path
- review and approval signals are materially conflicted
- authority-sensitive change cannot be justified inside current autonomy limits

---

## Strong-Reporting Mode

As approval sensitivity rises, reporting quality should rise too.

### Strong-reporting mode is appropriate when:

- approval is required for a significant action
- the action touches sensitive objects
- the path was denied and replanned
- escalation occurred
- a high-risk action is allowed to proceed

### Strong-reporting mode should improve:

- summary clarity
- rationale clarity
- actor visibility
- artifact reference quality
- state visibility
- next-step clarity

Strong reporting does not mean verbosity.
It means clearer accountable structure.

---

## Approval and Veto Relation

Approval denial and veto are related but not identical.

### Approval rejection

Means the current path does not have permission to proceed.

### Veto

Means the proposed path should not proceed as proposed because it is too unsound, too risky, too destructive, too unclear, or too overreaching.

A veto is stronger than ordinary approval rejection.

Typical consequences of veto:

- immediate stop of current path
- replan or escalate
- no casual retry of the same proposal

---

## Approval and Retry Relation

Do not treat approval as a retry loop.

If approval is rejected, the default should not be:

- resubmit the same path repeatedly
- rename the same path and try again

The default should be:

- revise the path
- reduce risk
- improve justification
- change the executor or scope if necessary
- escalate when current authority is insufficient

---

## Approval and Registry Changes

Registry changes often deserve stronger approval posture than ordinary edits.

Examples:

- permission changes
- risk ceiling changes
- lifecycle changes
- workflow activation
- authority-bearing metadata changes

These should usually not proceed as invisible low-risk mutations.

---

## Approval and Memory Changes

Durable memory changes may require approval when they are:

- destructive
- strategic
- difficult to reverse
- likely to alter future governance posture

Small additive durable memory updates may not require approval.
Destructive or authority-sensitive memory changes often should.

---

## Relation to Other Documents

This document should align with:

- `RISK_MODEL.md`
- `STATE_MACHINE.md`
- `WORKFLOW_REGISTRY_SPEC.md`
- `AGENT_REGISTRY_SPEC.md`
- `TRACE_SPEC.md`
- `policies/risk_policy.yaml`

This document defines approval semantics and control posture.

Future policy artifacts or validator logic may harden more of these rules.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- approval being confused with review
- significant actions proceeding without a permission gate
- workflow activation without approval
- sensitive changes being treated as ordinary low-risk edits
- repeated denial loops without replanning
- autonomy silently crossing authority boundaries
- high-risk continuation being treated as a normal approval checkbox

---

## Final Principle

Approval should exist exactly where permission matters.

Too little approval weakens governance.
Too much approval creates ceremonial drag.

The correct approval policy makes significant actions controllable without turning the whole system into bureaucracy.