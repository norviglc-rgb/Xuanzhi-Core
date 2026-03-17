# DEV_TASK_MODEL.md

## Purpose

This document defines the development task model of the Xuanzhi workspace.

Its purpose is to provide a stable semantic baseline for long-running development work, especially work delegated from Xuanzhi to Claude Code or other development executors.

This document is normative for:

- development work hierarchy
- development-unit meaning
- delivery expectations
- checkpoint and review logic
- bounded recovery logic
- phase-level reporting expectations

It is not a scheduler specification.
It is not a Git workflow manual.
It is not a full execution engine design.

Its job is to define the controlled shape of development work.

---

## Core Principle

A good development task model should make it clear:

- what unit of work is being discussed
- what level of completion is expected
- what kind of review or handoff should happen
- where recovery should happen after failure
- how long-running work remains governable

A bad development task model creates hierarchy without control value.

Therefore, this workspace uses hierarchy only where it improves:

- clarity
- recoverability
- delegation
- reporting
- checkpoint quality

---

## Canonical Hierarchy

The canonical long-running development hierarchy is:

`epic -> milestone -> task -> step`

Not every development request must use all four levels.

Use only the levels that add control value.

### Minimal usage rule

- small bounded work may use `task -> step`
- medium work may use `milestone -> task -> step`
- long-running complex work may use full `epic -> milestone -> task -> step`

Do not force simple work into unnecessary hierarchy.

---

## Unit Definitions

## Epic

An `epic` is the highest long-running development container.

Use an epic when the work:

- spans multiple meaningful milestones
- cannot be responsibly tracked as one flat task
- requires strategic continuity over time
- benefits from periodic checkpointing and governance review

An epic should answer:

- what larger objective is being pursued
- what major milestones define progress
- when the epic should be considered completed, paused, failed, or cancelled

### Epic should not be used for:

- one-shot small code changes
- short bounded fixes
- tasks that do not materially benefit from hierarchy

---

## Milestone

A `milestone` is a major delivery checkpoint inside an epic.

A milestone should produce something reviewable.

Typical milestone outcomes include:

- a completed implementation slice
- a validated prototype
- a refactor checkpoint
- a stable spec package
- a tested release candidate
- a decision-ready research result

A milestone exists to create a meaningful control point between “ongoing work” and “reviewable progress.”

### Milestone should answer:

- what bounded progress should be achieved
- what evidence demonstrates milestone completion
- what review or approval gate follows
- what happens if the milestone fails

---

## Task

A `task` is the main practical unit of development work.

A task should be:

- understandable
- bounded
- delegable
- reportable
- reviewable at outcome level

A task may be:

- a coding task
- a refactor task
- a bug-fix task
- a documentation/spec task
- a review task
- a setup or integration task

A task is the default top-level work unit when epic/milestone hierarchy is not needed.

### Task should answer:

- what is being attempted
- what deliverable is expected
- what constraints apply
- what counts as enough success for continuation or closure

---

## Step

A `step` is the smallest bounded controller-routable execution unit.

A step should normally have:

- a near-term goal
- a concrete action
- explicit success criteria
- rollback or recovery awareness
- bounded risk and resource hints

A step is not a long narrative.
It is not a whole project.
It is not a floating intention.

A step should be small enough to be:

- reasoned about
- routed
- reviewed
- retried
- replanned

### Step contract alignment

Where a formal step object is used, it should align with:

- `main-agent-step.schema.json`

---

## Deliverable Expectations by Level

## Epic deliverable

An epic should produce a major outcome or major sequence of validated outcomes.

Examples:

- a completed subsystem
- a major multi-stage implementation
- a stable and accepted architecture transition
- a release-ready capability family

### Epic deliverable form

Usually summary-level, milestone-linked, and strategic.

---

## Milestone deliverable

A milestone should produce a reviewable checkpoint.

Examples:

- code implemented and testable
- spec set revised and internally coherent
- pipeline built and validated
- integration milestone completed
- decision package ready for approval

### Milestone deliverable form

Concrete enough for review, not merely “work was done.”

---

## Task deliverable

A task should produce a direct practical result.

Examples:

- file changes
- tested fix
- refactor outcome
- short design output
- integration update
- implementation summary

### Task deliverable form

Task deliverables should be expressible in:

- `dev_result_packet.schema.json`
- status reporting
- artifact references
- review summary

---

## Step deliverable

A step should produce one bounded local outcome.

Examples:

- a file update
- a command result
- a patch proposal
- a validation result
- a short review finding
- a structured decision output

---

## Relationship to Executor Model

This workspace currently uses a bounded executor strategy.

### Xuanzhi

Xuanzhi is responsible for:

- framing development work
- delegating development work
- reviewing structured results
- preserving governance coherence
- summarizing progress
- handling escalation when needed

Xuanzhi is not the default heavy development executor.

### Claude Code

Claude Code is the default development executor.

Claude Code is expected to handle:

- long-running development execution
- implementation iteration
- code changes
- milestone progression
- internal development-team style coordination where useful

### Other systems

Other executors may support narrow or workflow-like parts of development,
but do not replace the main development executor role unless explicitly justified.

---

## Canonical Development Flow

A common long-running development flow is:

`intake -> planning -> task packet -> executor run -> result packet -> review -> next decision`

When hierarchy is used, this becomes:

`epic framing -> milestone planning -> task delegation -> step execution -> result review -> milestone decision -> epic continuation`

This model supports:

- clear delegation
- bounded execution
- structured reporting
- controlled failure handling

---

## Commit Rule

Meaningful development progression should produce commit-worthy checkpoints.

### Default rule

Each meaningful stage should commit.

This does not mean “every tiny keystroke.”

It means that meaningful progress slices should not remain uncheckpointed for too long.

### Why

Stage-level commits improve:

- recoverability
- reviewability
- traceability
- handoff clarity
- failure containment

This rule is especially important for long-running development work.

---

## Review Rule

Development work should not be considered complete merely because execution stopped.

Review is the checkpoint between “produced” and “accepted.”

### Typical review moments

- step result review where needed
- task result review
- milestone completion review
- delivery review before closure or merge

### Review questions

At minimum, review should consider:

- was the intended objective met
- is the result coherent
- did risk change
- are blockers explicit
- is the next step clear
- is the deliverable actually usable

---

## Failure and Recovery Rule

Failure should not immediately collapse the whole hierarchy unless the failure genuinely propagates upward.

### Step failure

Default next action:

- retry if bounded and justified
- otherwise replan the step or task path

### Task failure

Default next action:

- replan the task
- or escalate if the task cannot be responsibly resolved in the current path

### Milestone failure

Default next action:

- replan the milestone

Milestone failure does not automatically imply epic failure.

### Epic failure

Epic failure should be reserved for cases where the broader objective is no longer viable under the current constraints or governance posture.

---

## Retry Rule

Retries are bounded.

Default maximum:

`max_retry = 2`

This should be interpreted as bounded repetition of the same or near-identical failing path, not an invitation to rename the same failure repeatedly.

After retry limit is reached, the default next action is:

- replan
- or escalate if necessary

---

## Replan Rule

Replan is the normal recovery posture after bounded failure.

Replan should preserve:

- still-valid work
- still-valid assumptions
- useful artifacts
- useful lessons

Replan should replace:

- broken path logic
- failing execution shape
- poor executor fit
- invalid assumptions

Replan is not panic reset.
It is controlled redesign.

---

## Escalation Rule

Escalation should be used when:

- authority is insufficient
- risk is too high
- repeated recovery fails
- review conflict cannot be resolved locally
- milestone or task direction is no longer trustworthy
- human intervention is required by policy

Escalation is a governance mechanism, not a dramatic label.

---

## Long-Running Development Window

A single active run window for long-running development is treated as bounded.

Default active window:

`24 hours`

This means long-running development should be checkpointed and reviewed periodically rather than treated as one endless uninterrupted block.

Typical expectations after a long active window:

- progress summary
- checkpoint or commit
- blocker identification
- continuation decision

---

## Reporting Expectations

Long-running development must remain reportable.

At minimum, reporting should support visibility into:

- active epics
- active milestones
- active tasks
- running executors
- blockers
- stalled work
- recently completed work
- review outcomes
- replan or escalation events

The task model exists partly to make these reports meaningful.

---

## Development Unit Selection Guidance

### Use only `task -> step` when:

- the work is small and bounded
- failure does not require strategic regrouping
- review can happen at task level
- hierarchy would mostly add ceremony

### Use `milestone -> task -> step` when:

- the work has multiple bounded delivery checkpoints
- review quality matters between work slices
- task grouping meaningfully improves control

### Use full `epic -> milestone -> task -> step` when:

- the work is long-running
- the work spans multiple meaningful phases
- governance continuity matters across many sessions
- strategic checkpointing is necessary

Hierarchy should be earned by control value.

---

## Relation to Other Documents

This document should align with:

- `STATE_MACHINE.md`
- `RISK_MODEL.md`
- `TRACE_SPEC.md`
- `main-agent-step.schema.json`
- `contracts/dev_task_packet.schema.json`
- `contracts/dev_result_packet.schema.json`

This document defines development-unit meaning.

State behavior belongs in the state machine.
Risk posture belongs in the risk model.
Trace behavior belongs in the trace specification.

---

## Failure Modes This Model Should Prevent

This model exists partly to prevent:

- flat unstructured long-running work
- fake hierarchy with no control purpose
- milestone-less drift
- executor overload at the top layer
- repeated failure without bounded recovery
- work that cannot be summarized or reviewed coherently
- development progress that cannot be checkpointed

---

## Final Principle

A good development task model makes long-running work easier to govern, easier to recover, and easier to review.

If hierarchy does not improve control, it should not exist.

The correct model is not the most elaborate one.

It is the one that keeps development legible, delegated, and recoverable.