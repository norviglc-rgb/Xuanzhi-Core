# STATE_MACHINE.md

## Purpose

This document defines the runtime state model of the Xuanzhi workspace.

Its purpose is to provide a stable and explicit baseline for:

- task progression
- step progression
- review progression
- approval progression
- long-running development work
- retry, replan, and escalation behavior

This document is normative for runtime state semantics.

It is not a trace specification.
It is not a registry lifecycle specification.
It is not a full scheduler implementation manual.

Those belong in adjacent documents and policy artifacts.

---

## Core Principle

State exists to support control, not decoration.

A good state machine should:

- make progress legible
- make failure handling explicit
- make escalation predictable
- make reporting reliable
- make future machine-readable transition tables possible

A bad state machine invents too many states, hides responsibility, or mixes multiple state domains into one label.

Therefore, this workspace keeps state domains separate.

---

## State Domains

This workspace distinguishes the following domains:

- `task_state`
- `step_state`
- `review_state`
- `approval_state`
- `epic_state`
- `milestone_state`

These must not be collapsed casually into a single generic `state`.

### Why

Because they answer different questions:

- `task_state` -> what is the current runtime condition of the task?
- `step_state` -> what is the current runtime condition of the current bounded step?
- `review_state` -> what is the status of review?
- `approval_state` -> what is the status of approval?
- `epic_state` -> what is the current state of the long-running epic?
- `milestone_state` -> what is the current state of the current milestone?

---

## Task State Model

`task_state` is the main runtime condition of a task.

### Canonical task states

- `created`
- `intake`
- `planning`
- `planned`
- `running`
- `waiting_review`
- `waiting_approval`
- `waiting_external`
- `waiting_user`
- `waiting_resource`
- `paused`
- `blocked`
- `stalled`
- `replanning`
- `escalating`
- `completed`
- `failed`
- `cancelled`
- `archived`
- `cooldown`

### Task state meanings

#### `created`
The task exists but has not yet been meaningfully framed.

#### `intake`
The task is being interpreted, classified, and scoped.

#### `planning`
A workable path is being designed.

#### `planned`
A workable path has been produced and is ready to execute.

#### `running`
The task is actively progressing through execution.

#### `waiting_review`
Execution has reached a point where review is required before continuing or closing.

#### `waiting_approval`
Execution has reached a point where explicit approval is required before continuing.

#### `waiting_external`
The task is waiting on an external dependency.

Examples:

- external API result
- remote job completion
- third-party callback
- external system response

#### `waiting_user`
The task is waiting for direct user input or decision.

This should be used sparingly.

#### `waiting_resource`
The task is waiting for internal execution capacity or constrained resources.

Examples:

- executor slot
- branch or workspace lock
- runtime slot
- budget gate

#### `paused`
The task has been intentionally stopped for later continuation.

#### `blocked`
The task cannot proceed because a dependency, condition, or authority requirement is missing.

#### `stalled`
The task appears to have stopped making meaningful progress and requires inspection.

`stalled` is not identical to `failed`.

#### `replanning`
The system is designing a new path after mismatch, rejection, or failure.

#### `escalating`
The task is being routed to a stricter or higher-authority decision path.

#### `completed`
The task achieved a sufficient successful outcome.

#### `failed`
The task did not achieve a viable outcome on the current path.

#### `cancelled`
The task was intentionally terminated before successful completion.

#### `archived`
The task is closed and retained for history only.

#### `cooldown`
A short holding state after completion, failure, or major transition before the next governance action.

Use only when such cooling separation is operationally useful.

---

## Step State Model

`step_state` is the runtime condition of a bounded execution step.

### Canonical step states

- `step_created`
- `step_ready`
- `step_running`
- `step_waiting_review`
- `step_waiting_approval`
- `step_retrying`
- `step_replanned`
- `step_blocked`
- `step_completed`
- `step_failed`
- `step_cancelled`

### Step state meanings

#### `step_created`
The step has been defined but is not yet ready for execution.

#### `step_ready`
The step is prepared and may proceed.

#### `step_running`
The step is actively executing.

#### `step_waiting_review`
The step has produced an output that requires review.

#### `step_waiting_approval`
The step cannot continue without approval.

#### `step_retrying`
The step is being attempted again after a bounded failure.

#### `step_replanned`
The original step path was changed and a revised step is now in effect.

#### `step_blocked`
The step cannot proceed because a dependency or condition is missing.

#### `step_completed`
The step has succeeded.

#### `step_failed`
The step did not succeed and is not currently being retried.

#### `step_cancelled`
The step was intentionally terminated.

---

## Review State Model

`review_state` tracks result evaluation, not execution.

### Canonical review states

- `review_not_required`
- `review_pending`
- `review_running`
- `review_passed`
- `review_failed`
- `review_conflicted`

### Review state meanings

#### `review_not_required`
No review is required for the current context.

#### `review_pending`
Review is required but has not started.

#### `review_running`
Review is actively in progress.

#### `review_passed`
The result passed review sufficiently.

#### `review_failed`
The result did not pass review.

Default downstream action is usually replan rather than blind continuation.

#### `review_conflicted`
Review signals are materially inconsistent and need a stricter decision path.

Typical downstream action is escalation or governance arbitration.

---

## Approval State Model

`approval_state` tracks permission gating, not output quality.

### Canonical approval states

- `approval_not_required`
- `approval_pending`
- `approval_running`
- `approval_granted`
- `approval_rejected`
- `approval_escalated`

### Approval state meanings

#### `approval_not_required`
No approval is required for the current context.

#### `approval_pending`
Approval is required but not yet started.

#### `approval_running`
Approval evaluation is currently in progress.

#### `approval_granted`
Permission to proceed has been granted.

#### `approval_rejected`
Permission to proceed has been denied.

Default downstream action is usually replan unless policy requires cancellation or escalation.

#### `approval_escalated`
Approval cannot be resolved in the current path and has been escalated.

---

## Long-Running Development State Model

Long-running development work may use:

- `epic_state`
- `milestone_state`
- `task_state`
- `step_state`

This hierarchy should only be used when the work materially benefits from it.

Do not force every task into epic/milestone structure.

### Epic states

Preferred `epic_state` values:

- `epic_created`
- `epic_running`
- `epic_paused`
- `epic_blocked`
- `epic_completed`
- `epic_failed`
- `epic_cancelled`
- `epic_archived`

### Milestone states

Preferred `milestone_state` values:

- `milestone_created`
- `milestone_running`
- `milestone_waiting_review`
- `milestone_waiting_approval`
- `milestone_blocked`
- `milestone_replanning`
- `milestone_completed`
- `milestone_failed`
- `milestone_cancelled`

### Long-running hierarchy rule

A failure at a lower level does not automatically imply total epic failure.

Examples:

- a step may fail, then replan
- a milestone may fail, then replan
- an epic may continue with revised milestone structure

The system should preserve room for controlled recovery before escalating to global failure.

---

## Canonical Progression Logic

### Normal task progression

Typical path:

`created -> intake -> planning -> planned -> running -> completed`

### Review-gated progression

Typical path:

`running -> waiting_review -> running or completed`

### Approval-gated progression

Typical path:

`running -> waiting_approval -> running or replanning`

### External wait progression

Typical path:

`running -> waiting_external -> running`

### Resource wait progression

Typical path:

`planned or running -> waiting_resource -> running`

### Pause and resume progression

Typical path:

`running -> paused -> running`

### Failure and recovery progression

Typical path:

`running -> failed -> replanning -> planned or running`

### Escalation progression

Typical path:

`waiting_review or waiting_approval or failed -> escalating -> replanning or cancelled`

---

## Retry Rule

Retries are bounded.

### Default retry limit

`max_retry = 2`

This means the system should not keep retrying the same failing step or path indefinitely.

### Retry scope

Retries should be interpreted narrowly.

The default meaning is:

- retry the same step or near-identical step pattern up to the bounded limit
- do not disguise repeated failure by renaming the same failing pattern

### Retry after limit

When the retry limit is reached, the default next action is not another blind retry.

The default next action is:

- `replanning`
- or `escalating` if the failure is serious enough

### Retry rule for review and approval failure

- review failure -> default next action is `replanning`
- approval rejection -> default next action is `replanning`
- repeated unresolved conflict -> consider `escalating`

---

## Replan Rule

Replan is the default recovery posture for bounded failure.

Replan is appropriate after:

- milestone failure
- review failure
- approval rejection
- repeated bounded step failure
- a path proving structurally unsound
- major context or constraint change

Replan does not mean “start over blindly.”

It means:

- preserve what is still valid
- replace what failed
- revise path quality
- maintain traceability of the change

---

## Escalation Rule

Escalation is used when the current governance path is insufficient.

Escalation is appropriate when:

- risk is too high
- authority is insufficient
- review is materially conflicted
- repeated failure persists after bounded recovery attempts
- destructive or structurally important decisions cannot be resolved locally
- human intervention is required by policy

Escalation should not be used as the default substitute for thoughtful replanning.

---

## Stalled Rule

`stalled` is a diagnosis state, not a generic synonym for `failed`.

A task should be considered stalled when it appears to have stopped making meaningful progress and the reason is not already captured by another clearer state such as:

- `waiting_external`
- `waiting_user`
- `waiting_resource`
- `blocked`
- `paused`

### Default stalled threshold

`2 hours`

This threshold should be treated as an operational default, not a metaphysical truth.

### Before marking stalled

The system should first check whether the task is actually:

- waiting on an expected dependency
- paused intentionally
- blocked for a known reason
- still receiving valid heartbeat without progress signal

Only then should `stalled` be applied.

---

## Long-Running Active Window

The default single active run window for long-running work is:

`24 hours`

This does not mean the total project must finish in 24 hours.

It means the system should treat each active run window as bounded and reviewable.

After a long active window, the system should expect:

- checkpointing
- progress summary
- review point
- continuation decision

---

## Controller Scan Cadence

Default controller scan cadence:

`5 minutes`

This cadence is intended to support:

- stalled detection
- waiting-state inspection
- approval/review progress checks
- long-task supervision
- basic scheduler visibility

This document does not define the full scheduler implementation.

It defines the expected timing posture.

---

## Parallel Step Rule

Parallel steps are allowed.

But parallelism is never free.

Parallel execution requires explicit consideration of:

- resource scheduling
- workspace or repo locks
- environment conflicts
- agent slot limits
- collision risk
- deadlock risk

### Parallel step guidance

Use parallel steps only when:

- the work is actually separable
- the execution environments are safely isolated
- the coordination overhead is justified
- rollback complexity remains manageable

If these are not true, sequential execution is preferred.

---

## Deadlock and Lock Awareness

This state document does not define full lock semantics.

However, it establishes the runtime principle that:

- lock pressure may produce `waiting_resource`
- conflicting resource claims may produce `blocked`
- unresolved execution stagnation may later produce `stalled`

Detailed lock design should live in a dedicated locking or scheduler specification.

---

## Reporting Expectations

The state machine exists partly to support reliable reporting.

At minimum, daily reporting should be able to surface:

- running tasks
- running agents
- blocked tasks
- stalled tasks
- waiting approvals
- recent failures
- recent completions

This document does not define report templates.
It defines the state visibility that reports depend on.

---

## State Design Rules

### Rule 1: Separate state domains

Do not merge task, step, review, approval, and lifecycle states.

### Rule 2: Prefer meaningful states over decorative states

Every state should justify its existence by improving control or reporting.

### Rule 3: Prefer explicit wait reasons

Use `waiting_external`, `waiting_user`, and `waiting_resource` when those reasons are known.

Do not hide them inside vague generic states.

### Rule 4: Failure should tend toward replan before chaos

Bounded failure should normally lead to controlled recovery rather than immediate uncontrolled escalation.

### Rule 5: Escalation is a stricter path, not a synonym for seriousness

Use escalation when current authority or governance is insufficient, not merely because something feels difficult.

---

## Relation to Other Documents

This document should align with:

- `RISK_MODEL.md`
- `TRACE_SPEC.md`
- `DEV_TASK_MODEL.md`
- `contracts/dev_task_packet.schema.json`
- `contracts/dev_result_packet.schema.json`
- `main-agent-step.schema.json`
- future `policies/state_transitions.yaml`

This document defines state meaning.
The machine-readable transition table should define enforceable allowed transitions.

---

## Final Principle

A good state machine makes the system easier to govern, easier to recover, and easier to report on.

If states multiply without improving control, the model is drifting.

The correct state model is not the most elaborate one.

It is the one that makes progress, blockage, recovery, and escalation legible.