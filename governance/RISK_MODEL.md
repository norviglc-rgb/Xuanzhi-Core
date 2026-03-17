# RISK_MODEL.md

## Purpose

This document defines the risk model of the Xuanzhi workspace.

Its purpose is to provide a stable baseline for:

- risk classification
- bounded execution
- approval posture
- escalation posture
- veto conditions
- sensitive-object handling
- future machine-readable risk policy

This document is normative for risk semantics.

It is not a full policy engine implementation.
It is not a substitute for machine-readable policy.
It is not a generic essay about danger.

Its job is to define what risk means in this workspace and how the system should respond to it.

---

## Core Principle

Risk is not an ornament attached after execution planning.

Risk is part of task framing.

A useful risk model should help the system answer:

- how dangerous is this path
- how reversible is this path
- how sensitive is the target
- how much authority is required
- whether execution should proceed, pause, replan, escalate, or stop

A bad risk model creates labels without changing behavior.

Therefore this workspace treats risk as behavior-shaping, not merely descriptive.

---

## Risk Dimensions

Risk should be judged from a combination of factors, including:

- reversibility
- destructive potential
- sensitivity of the target
- authority implications
- scope of impact
- cost and resource impact
- uncertainty level
- recoverability
- downstream maintenance burden

Not every risk judgment requires a formal score,
but all meaningful risk judgments should reflect these dimensions implicitly or explicitly.

---

## Canonical Risk Levels

This workspace recognizes five categorical risk levels:

- `R0`
- `R1`
- `R2`
- `R3`
- `R4`

These levels are governance categories, not mere descriptive decorations.

They are expected to influence routing, approval, escalation, and execution posture.

---

## Risk Level Meanings

### `R0`

Read-only, low-impact, or near-zero-side-effect work.

Typical examples:

- retrieval
- lightweight summarization
- low-stakes planning
- non-destructive analysis
- metadata inspection
- review without mutation

Typical posture:

- proceed normally
- approval usually not required
- escalation usually not required

### `R1`

Low-risk reversible modification with bounded local impact.

Typical examples:

- small reversible edits
- local non-sensitive file changes
- low-risk draft generation
- low-risk task shaping
- internal organization changes with easy rollback

Typical posture:

- proceed with ordinary caution
- approval may still be unnecessary
- rollback should be straightforward

### `R2`

Meaningful change with non-trivial impact, broader scope, or moderate uncertainty.

Typical examples:

- substantial code changes
- workflow changes with visible downstream effects
- memory writes with durable influence
- changes that affect project behavior or cost
- non-trivial structural refactors
- integration changes with moderate blast radius

Typical posture:

- review is often appropriate
- approval may be required depending on sensitivity
- executor fit matters more strongly
- rollback and trace should be clearer

### `R3`

High-risk, sensitive, destructive, authority-heavy, or hard-to-reverse work.

Typical examples:

- changes to critical configuration
- changes affecting registries, durable governance, or control surfaces
- sensitive memory deletion or rewrite
- workflow activation or permission-sensitive transitions
- high-cost actions with significant downside
- actions touching security-relevant or runtime-critical infrastructure
- actions with broad blast radius or low recoverability

Typical posture:

- elevated caution required
- approval is often required
- governance review is stronger
- escalation becomes more likely
- execution should not proceed casually

### `R4`

Emergency block class.

`R4` is used for actions that should not proceed on the normal execution path.

Typical examples:

- clearly destructive and unjustified actions
- clearly unauthorized or overreach actions
- actions with extreme downside and inadequate information
- actions that materially threaten system integrity or authority boundaries
- paths that require human intervention before any execution should continue

Typical posture:

- immediate stop
- do not continue as a normal executable path
- escalate
- require human or stricter governance resolution

---

## Risk Score

`risk_score` is the more granular companion to `risk_level`.

### Role of `risk_score`

Use `risk_score` when a finer distinction is useful.

Examples:

- ranking alternatives
- deciding between low and medium caution within a risk class
- future policy or reporting support

### Role of `risk_score_hint`

Use `risk_score_hint` when the score is advisory and estimated by the main agent rather than final and authoritative.

### Principle

Categorical risk drives posture.
Numeric risk refines judgment.

Do not use a numeric score as camouflage for unclear reasoning.

---

## Sensitive Objects

The following are considered sensitive object classes in this workspace:

- memory
- knowledge
- configuration
- CI/CD
- nginx or equivalent gateway/runtime configuration
- docker runtime or equivalent execution substrate
- registries
- workflow activation surfaces
- permission-bearing objects
- sub-agent authority expansion

This list may expand later,
but these categories are already sensitive enough to justify explicit caution.

### Sensitive object rule

Touching a sensitive object does not automatically make a task `R4`.

But it should raise scrutiny and often increases the minimum likely risk level.

---

## Destructive Actions

A destructive action is any action that may:

- delete
- overwrite
- revoke
- corrupt
- disable
- misconfigure
- materially reduce recoverability
- irreversibly degrade useful state

Examples:

- deleting durable memory
- changing critical runtime configuration
- removing or replacing important workflow definitions
- modifying sensitive registries without proper review
- broad destructive file operations

### Destructive action rule

The presence of destructive potential should raise risk posture significantly.

A destructive action with poor justification, poor reversibility, or poor authority fit may trigger veto or `R4`.

---

## Authority-Sensitive Actions

An action is authority-sensitive when it affects:

- permissions
- registry admission
- lifecycle activation
- durable governance state
- approval requirements
- executor authority boundaries
- sub-agent creation or expansion with meaningful capability changes

These actions should not be treated as ordinary low-risk edits.

---

## Risk and Uncertainty

Uncertainty is itself a risk multiplier.

If the system does not adequately know:

- what will change
- what the blast radius is
- who owns the target
- how to reverse the action
- whether the action is authorized
- whether the requested outcome is actually beneficial

then risk posture should rise, not fall.

### Principle

Low information plus high impact is not normal execution.
It is a caution or escalation case.

---

## Veto Rule

Xuanzhi may veto a proposed path when the path is:

- clearly destructive without sufficient justification
- clearly unauthorized or overreaching
- clearly low-ROI relative to cost and complexity
- clearly under-specified with meaningful downside
- clearly in conflict with durable system integrity

A veto is not the same as ordinary rejection.

A veto means:

- the current path should not proceed as proposed
- normal execution should stop
- a safer alternative, replan, or escalation is required

### Review-agent limitation

A review-oriented actor may recommend blocking or escalation,
but does not hold final veto authority by default.

Final veto authority belongs to the governance core or stricter governance path.

---

## Approval Posture by Risk Level

These are default tendencies, not a substitute for policy detail.

### `R0`

- approval usually not required
- ordinary execution posture

### `R1`

- approval often not required
- normal caution
- easy rollback expected

### `R2`

- approval may be required depending on sensitivity and durability
- review is often useful
- more structured reporting is appropriate

### `R3`

- approval commonly required
- stronger governance review expected
- routing and executor fit matter strongly
- escalation becomes more likely

### `R4`

- do not treat as normal approvable execution
- immediate stop and escalate
- human or stricter governance intervention is typically required

---

## Escalation Triggers

Escalation should be strongly considered when:

- the action is `R4`
- the action is `R3` with unresolved uncertainty
- the action touches highly sensitive objects with weak information
- repeated attempts fail after bounded recovery
- authority cannot be established clearly
- review results are materially conflicted
- approval cannot be resolved in the current path
- the system may be about to overreach its allowed role

Escalation is not failure theatre.
It is a governance control response.

---

## Replan Triggers

Replan is preferred over blind repetition when:

- the current path failed
- review failed
- approval was rejected
- assumptions proved wrong
- the selected executor was a poor fit
- risk increased materially
- the original scope was unrealistic

Risk should not merely classify outcomes.
It should shape better next paths.

---

## Risk and Executor Fit

Risk is partly about who performs the action.

The same action may carry different practical risk depending on the executor.

Examples:

- top-layer handling may be too weak for heavy development execution
- a specialized executor may reduce operational risk through better fit
- a poorly matched executor may increase risk even for a nominally moderate task

Therefore:

risk is not only about the action  
it is also about action-executor fit

---

## Risk and Memory

Memory-related operations deserve special caution because they affect future judgment.

### Low-risk memory actions

Examples:

- adding a compact stable preference
- adding a small durable navigation summary

These may be `R1` or `R2` depending on impact.

### Higher-risk memory actions

Examples:

- deleting durable memory
- rewriting long-term memory categories
- changing strategic lessons
- altering memory in ways that affect governance posture

These are more likely to be `R2` or `R3`.

Poorly justified destructive memory action may rise to `R4`.

---

## Risk and Registries

Registry and activation-related work is sensitive by default.

Examples:

- admitting a new governed agent
- changing authority-relevant metadata
- activating workflows
- changing workflow permissions
- modifying lifecycle state of durable controlled objects

These should usually not be treated as casual low-risk edits.

Risk classification should consider:

- authority
- blast radius
- reversibility
- reporting requirements

---

## Risk and Runtime/Infrastructure

Changes affecting runtime or infrastructure surfaces should be treated with elevated caution.

Examples:

- nginx or gateway routing changes
- Docker runtime changes
- CI/CD pipeline changes
- sensitive environment or deployment configuration changes

These often justify `R2` or `R3`,
and in some cases may justify `R4` if the path is clearly unsafe or unauthorized.

---

## Reporting Expectations

Risk should influence reporting intensity.

As risk rises, the system should generally increase:

- explicit summary quality
- trace clarity
- rationale visibility
- review visibility
- escalation visibility

High-risk action without strong reporting is governance weakness.

This does not mean verbose storytelling.
It means clearer structured accountability.

---

## Relation to Step and Packet Contracts

This document should align with:

- `main-agent-step.schema.json`
- `contracts/dev_task_packet.schema.json`
- `contracts/dev_result_packet.schema.json`

### Important note about `R4`

The workspace recognizes `R4` at the overall risk-model level.

However, some executable step contracts may intentionally exclude `R4` because `R4` is a block/escalation class rather than a normal executable-step class.

This is an intentional design distinction, not a contradiction.

---

## Relation to Future Policy

This document defines risk meaning and governance posture.

Future machine-readable artifacts should define enforceable rules such as:

- `risk_policy.yaml`
- approval rules
- validator checks
- executor gating logic

This document is the semantic baseline, not the final enforcement layer.

---

## Failure Modes This Model Should Prevent

This model exists partly to prevent the following:

- treating all execution as equivalent
- using risk labels without changing behavior
- normalizing destructive or authority-sensitive actions
- mistaking uncertainty for safety
- continuing obviously bad paths because an executor exists
- allowing high-risk work to proceed with weak review or reporting
- confusing veto with ordinary task failure

---

## Final Principle

A useful risk model changes behavior.

If a risk classification does not affect routing, approval, review, escalation, or execution posture, it is only decoration.

This workspace treats risk as a control surface, not a label collection.