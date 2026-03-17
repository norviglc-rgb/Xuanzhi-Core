# CLAUDE_CODE_EXECUTION_SPEC.md

## Purpose

This document defines how Claude Code is used as the default development executor in the Xuanzhi workspace.

Its purpose is to provide a stable execution integration baseline for:

- long-running development work
- repository-local implementation
- structured handoff from Xuanzhi
- bounded execution and reporting
- development checkpointing
- recovery after failure
- alignment with repo, review, and merge flow

This document is normative for Claude Code execution posture.

It is not a prompt file.
It is not a full Claude Code product manual.
It is not a substitute for repository governance, risk policy, or runtime trace.

Its job is to define how Claude Code should fit into the governed execution model.

---

## Core Principle

Claude Code is the default development executor, not the governance core.

Xuanzhi governs.
Claude Code executes development.

A good integration should make it clear:

- when work should be delegated to Claude Code
- what information Claude Code should receive
- what Claude Code should be expected to produce
- when checkpoints, review, or escalation should happen
- how long-running development remains governable

A bad integration turns Claude Code into either:

- an unbounded autonomous black box
or
- a tightly micromanaged top-layer burden

This workspace prefers bounded delegated execution.

---

## Role of Claude Code

Claude Code is the default executor for implementation-heavy development work.

It is best suited for:

- long-running software development
- code changes inside repositories
- iterative implementation and testing
- bounded refactor work
- development milestone progression
- internal development-team style coordination where useful

Claude Code is not the final governance authority.

Claude Code does not replace:

- Xuanzhi task framing
- Xuanzhi routing
- Xuanzhi risk-aware control posture
- Xuanzhi summary and reporting role
- approval or escalation gates

---

## When to Use Claude Code

Claude Code should usually be selected when work is mainly:

- development-heavy
- repository-centered
- long-running
- implementation-focused
- iterative and test-driven
- likely to benefit from subtask decomposition or internal execution coordination

Examples:

- implementing a feature
- fixing a bug
- performing a non-trivial refactor
- updating code plus tests
- carrying out a multi-step development milestone
- executing a bounded development spike or prototype

Claude Code should not be the default choice for:

- pure governance reasoning
- lightweight summarization
- low-risk read-only inspection
- simple planning with no heavy execution
- tasks better handled by existing workflow systems
- tasks that are primarily publishing, media generation, or narrow external automation

---

## Relationship to Xuanzhi

Xuanzhi remains the control plane.

### Xuanzhi responsibilities

Xuanzhi is responsible for:

- understanding the user's real task
- framing the development work
- selecting Claude Code when appropriate
- assigning risk and approval posture
- deciding what success means
- summarizing progress and outcomes
- deciding when to review, replan, escalate, or stop
- maintaining summary-level memory and reporting

### Claude Code responsibilities

Claude Code is responsible for:

- executing delegated development work
- operating inside the repo-local work context
- producing code and related artifacts
- checkpointing meaningful progress
- reporting bounded results back to Xuanzhi
- surfacing blockers clearly
- proposing next steps when useful

### Principle

Xuanzhi should not micromanage every keystroke.

Claude Code should not silently become self-governing.

---

## Canonical Handoff Model

The preferred handoff path is:

Xuanzhi -> development task packet -> Claude Code -> development result packet -> Xuanzhi review

### Preferred packet contracts

This integration should align with:

- `contracts/dev_task_packet.schema.json`
- `contracts/dev_result_packet.schema.json`

### Optional step-level structure

Where finer-grained controller-routable step planning is used, it should align with:

- `main-agent-step.schema.json`

### Handoff principle

Xuanzhi should pass:

- what the task is
- what the goal is
- what the deliverable is
- what constraints apply
- what approval or risk posture applies
- what reporting is required

Claude Code should return:

- what was done
- current status
- changed artifacts
- test/build results when relevant
- blockers
- next-step recommendation when useful

---

## Repository Execution Posture

Claude Code should operate inside a clear repository context.

### Repo-local clarity expectations

The repo should make it easy for Claude Code to identify:

- code location
- test location
- docs location
- scripts location
- repo-local governance location

This should align with the repository template baseline.

### Repo-local execution principle

Claude Code should work inside the repo shape rather than forcing the repo to adapt to improvisational execution behavior.

Where project structure is unclear, Xuanzhi should prefer clarifying or normalizing the repo structure rather than allowing silent structural drift.

---

## Stage Commit Policy

Meaningful development progression should be checkpointed.

### Default rule

Each meaningful stage should commit.

This does not mean every tiny edit requires a commit.

It means that meaningful work slices should not remain uncheckpointed for too long during long-running development.

### Why

Stage commits improve:

- recoverability
- reviewability
- traceability
- comparison against prior state
- replan quality after failure

### Practical interpretation

A meaningful stage is usually one that changes one of the following:

- behavior
- structure
- tests
- integration surface
- milestone progress posture

---

## Milestone Summary Policy

When a milestone boundary is reached, Claude Code should be able to produce a bounded milestone summary.

A milestone summary should make it clear:

- what was attempted
- what was completed
- what artifacts changed
- what was validated
- what remains blocked or uncertain
- what the next decision point is

The summary should be concise and reviewable.

It should not be a giant development diary.

---

## Review Integration

Claude Code execution output should be suitable for later review.

### Review expectations

Results from Claude Code should support review of:

- objective fit
- code or artifact coherence
- validation status
- blocker clarity
- risk changes
- continuation readiness

### Review principle

Claude Code should produce development output that can be reviewed.

It should not require Xuanzhi to reconstruct the entire context from raw sprawl.

---

## Failure and Recovery Posture

Claude Code is part of a bounded recovery model.

### Step or task failure

If execution fails at a bounded level, the default next action is usually:

- retry if the path is still justified and within retry bounds
- otherwise replan

### Milestone failure

Default next action:

- replan the milestone

Milestone failure does not automatically imply whole-project failure.

### Repeated failure

When bounded retries are exhausted, the normal next action is not blind persistence.

The normal next action is:

- replan
- or escalate if the path is too risky or too unclear

### Principle

Claude Code is expected to surface failure clearly, not hide it inside narrative optimism.

---

## Long-Running Development Window

Long-running development should be treated as bounded active windows, not endless uninterrupted flow.

Default active window:

`24 hours`

After a long active window, the system should expect:

- checkpoint or commit
- progress summary
- blocker status
- continuation decision

Claude Code does not need to stop existing work at exactly the boundary,
but the governance model expects periodic reviewable checkpoints.

---

## Reporting Expectations

Claude Code should return results in a structure that supports Xuanzhi's reporting role.

At minimum, reporting should be able to preserve:

- task summary
- status summary
- changed files or artifact references
- tests/checks run
- blockers
- next-step recommendation where useful

### Reporting principle

Prefer:

- concise summaries
- artifact references
- bounded notes

Avoid:

- giant raw transcripts
- unfiltered implementation chatter
- verbose self-justification dumps

---

## Branch and Merge Posture

Claude Code should operate in a branch-aware development flow.

The default governed path remains:

Issue -> Branch -> MR -> CI -> Review -> Merge

### Branch expectations

Where branch policy applies, Claude Code should follow the relevant branch family and work in a branch-scoped path rather than mutating shared surfaces carelessly.

### Merge principle

Claude Code may prepare work for merge,
but merge remains governed by CI, review, and approval posture where applicable.

---

## Testing and Validation Posture

Claude Code should validate development output whenever validation is relevant and feasible.

Typical validation expectations include:

- tests
- lint
- build checks
- bounded verification commands
- explicit note when validation could not be completed

### Principle

A development result without validation signal is weaker than one with explicit validation posture.

If validation is not run, that should be stated clearly rather than implied away.

---

## Internal Teaming Inside Claude Code

Internal task decomposition or development-team style coordination may happen inside Claude Code when it improves execution.

This is acceptable as long as:

- Xuanzhi remains the governance control plane
- Claude Code remains inside bounded execution scope
- outputs remain structured and reviewable
- authority does not silently expand
- trace and summary quality remain adequate

### Principle

Internal coordination is a tool of execution quality,
not an excuse to move governance upward or sideways.

---

## Risk and Approval Interaction

Claude Code execution does not bypass risk or approval posture.

If a delegated task carries:

- elevated risk
- destructive potential
- authority-sensitive consequences
- merge or activation gates
- structurally important change

then execution should remain subject to the relevant review, approval, or escalation path.

### Principle

Executor competence is not permission.

---

## Repo-Local Governance Awareness

Where a repo contains project-local governance under `/.governance`,
Claude Code should treat it as repo-local operational context rather than global workspace policy.

### Layer distinction

- workspace-level governance -> main Xuanzhi workspace
- repo-local governance -> target repository

Claude Code should not silently rewrite governance layers without explicit task fit and permission.

---

## Integration Boundary

This document intentionally does not define:

- full Claude Code prompt content
- full Claude Code installation process
- all Claude Code commands or flags
- low-level runtime container details
- controller implementation code
- GitLab API specifics

Those belong in:

- product documentation
- operational runbooks
- GitLab integration specs
- implementation-level setup or deployment docs

This document stays useful only if it remains execution-posture focused.

---

## Relation to Other Documents

This document should align with:

- `DEV_TASK_MODEL.md`
- `STATE_MACHINE.md`
- `RISK_MODEL.md`
- `TRACE_SPEC.md`
- `REPO_TEMPLATE_SPEC.md`
- `contracts/dev_task_packet.schema.json`
- `contracts/dev_result_packet.schema.json`

This document defines Claude Code execution posture.

It does not replace risk, state, packet, or repo governance documents.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- top-layer execution overload
- repo-local development without governance framing
- long-running development with no checkpoints
- development output too noisy to review
- repeated failure without bounded recovery
- branchless or structure-blind execution drift
- executor capability being mistaken for approval authority

---

## Final Principle

Claude Code should carry the heavy development work, not the governance burden.

The correct integration keeps Xuanzhi in control, keeps Claude Code effective, and keeps long-running development legible, checkpointed, and reviewable.