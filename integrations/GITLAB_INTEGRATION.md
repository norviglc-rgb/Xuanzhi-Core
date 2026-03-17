# GITLAB_INTEGRATION.md

## Purpose

This document defines how GitLab CE is integrated into the Xuanzhi workspace as the primary repository, issue, merge, and CI control surface for governed development work.

Its purpose is to provide a stable integration baseline for:

- repository creation
- issue-driven development flow
- branch discipline
- merge request discipline
- CI gating
- review and delivery checkpoints
- governance-compatible development traceability

This document is normative for GitLab integration posture.

It is not a GitLab API reference.
It is not a CI pipeline file.
It is not a substitute for repo template, risk policy, or approval policy.

Its job is to define how GitLab fits into the governed development model.

---

## Core Principle

GitLab is not just code storage.

In this workspace, GitLab is a development control surface.

A good integration should make it clear:

- how work enters repo flow
- how development work is tracked
- how change is isolated
- how review and CI gates work
- how merge remains governed
- how repo state supports reporting and recovery

A bad integration treats GitLab as a passive file bucket and leaves governance to informal habit.

This workspace prefers explicit, reviewable, issue-linked development flow.

---

## Role of GitLab

GitLab CE is the primary system of record for repository-centered development work.

GitLab is used for:

- repository hosting
- issue tracking
- branch-based change isolation
- merge request workflow
- CI execution and gating
- change review checkpoints
- development traceability support

GitLab is not the top governance core.

Xuanzhi remains responsible for:

- task framing
- routing
- risk-aware control
- approval posture
- summary and reporting
- escalation decisions

Claude Code remains the default development executor.

GitLab is the primary repo and change-control surface around that execution.

---

## Repository Creation Posture

Xuanzhi may create repositories automatically where policy allows.

### Automatic creation should still preserve

- project type selection
- repo naming clarity
- template fit
- baseline directory structure
- CI baseline
- branch naming baseline
- project-local governance placement

### Principle

Automatic repo creation is allowed only as governed creation,
not as unstructured repo proliferation.

Repository creation should align with:

- `REPO_TEMPLATE_SPEC.md`

---

## Issue-Driven Development Flow

The default governed development path is:

`Issue -> Branch -> MR -> CI -> Review -> Merge`

This should be treated as the standard control path for repo-centered work.

### Issue role

Issues should serve as the primary bounded record for:

- requested work
- scoped change intent
- defect description
- research question
- governance-related repo work

### Default issue categories

At minimum, the following issue categories should exist:

- `feature`
- `bug`
- `task`
- `research`
- `governance`

### Principle

Work should not drift into major repo changes with no issue-level framing unless the work is genuinely too small to justify it.

---

## Branch Discipline

Branches are the default isolation surface for governed change.

### Default branch families

- `feature/*`
- `fix/*`
- `research/*`
- `infra/*`
- `experiment/*`

### Branch purpose

Branches should communicate:

- intent
- scope posture
- type of work

### Branch rule

Meaningful work should not happen directly on a shared mainline path without branch-aware isolation unless policy explicitly allows it for a very small bounded case.

### Principle

Branching is not bureaucracy.
It is change isolation.

---

## Merge Request Discipline

Merge requests are the primary structured review surface for code and governed repo changes.

### MR role

An MR should make it easier to answer:

- what changed
- why it changed
- whether CI passed
- whether the work should merge
- whether risk or approval posture changed

### MR expectation

Meaningful repo changes should normally arrive through MR rather than silent direct merge.

### MR should support

- review
- delivery review
- CI status visibility
- linkage to issue context
- bounded summary of change intent

---

## CI Baseline

The default CI baseline should include:

- lint
- test
- build
- security scan

The exact implementation may vary by project type,
but the governance expectation remains.

### CI gate rule

CI failure should block merge by default.

### Why

This preserves:

- delivery discipline
- quality gating
- recoverability
- review confidence

### Principle

CI is not cosmetic.
CI is part of governed merge posture.

---

## Review Integration

GitLab MR flow should support both review and delivery review.

### Review surfaces

Typical review may include:

- code review
- structure review
- delivery readiness review
- test/build result review
- risk-aware review when relevant

### Review actors

Review may be performed by:

- review agents
- delivery review agents
- humans when risk, ambiguity, or repeated failure justify escalation

### Principle

GitLab should make review legible.
It should not hide review behind informal chat-only approval.

---

## Merge Posture

Merge should occur only after the relevant gates are satisfied.

Typical merge expectations include:

- issue context exists where appropriate
- branch isolation was used where appropriate
- MR exists for meaningful changes
- CI passed
- required review posture is satisfied
- required approval posture is satisfied

### Merge rule

Merge is not the same thing as code existence.

Merge is a governance checkpoint that says:

this change is accepted into shared durable project truth

---

## Development Executor Interaction

Claude Code is the default development executor for repo-centered implementation work.

### Claude Code should interact with GitLab through governed flow

Typical shape:

- work framed by Xuanzhi
- issue or bounded task context identified
- branch created or selected
- repo-local implementation performed
- commits produced at meaningful checkpoints
- MR prepared where appropriate
- CI and review gates observed
- merge occurs only through the governed path

### Principle

GitLab provides the durable change-control path around executor activity.

---

## Commit Discipline

Meaningful development progression should produce commit-worthy checkpoints.

### Commit expectations

Commits should support:

- recoverability
- reviewability
- comparison against prior state
- bounded progress visibility

### Principle

A repo history full of giant unstructured dumps weakens control.
A repo history full of coherent checkpoints improves it.

This aligns with the workspace stage commit policy.

---

## Repo-Local Governance

Projects may contain repo-local governance material under:

- `/.governance`

GitLab should treat this as repo-local controlled content, not as a replacement for workspace-wide governance.

### Principle

Repo-local governance belongs in the repo.
Workspace-wide governance belongs in the main Xuanzhi workspace.

Do not silently collapse these layers.

---

## Risk and Approval Interaction

GitLab flow does not override risk or approval policy.

A branch, commit, or MR existing does not mean the change is allowed to proceed to merge.

### Practical rule

When work is:

- high-risk
- destructive
- authority-sensitive
- registry-affecting
- workflow-activating
- infra-sensitive

merge posture should remain subject to the relevant review, approval, or escalation path.

### Principle

GitLab flow is necessary, but not sufficient, for governance.

---

## Workflow and Registry Changes in Git Repos

Some repos may contain workflow definitions, agent definitions, or project-local governance files.

These changes may require stronger scrutiny than ordinary source-code edits.

Examples:

- workflow definition changes
- activation-adjacent config changes
- project-local approval changes
- project-local governance policy changes
- permission-relevant config changes

These should not be treated as ordinary low-risk formatting edits merely because they live in a repository.

---

## Release-Like or Delivery-Like Readiness

For work that functions as a delivery checkpoint,
GitLab should support a final readiness posture before merge or release-like completion.

Typical questions include:

- did CI pass
- did review pass
- are blockers resolved
- is risk posture acceptable
- is the repo state coherent enough to accept the change

This is not necessarily a separate GitLab feature.
It is a governed use of GitLab surfaces.

---

## Traceability Support

GitLab should support governance traceability indirectly through:

- issue linkage
- branch naming
- MR structure
- commit history
- CI results
- merge record

GitLab is not the only trace surface,
but it is a major artifact source for development-related trace and review.

### Principle

Prefer referencing GitLab artifacts from trace and reporting rather than duplicating their full contents elsewhere.

---

## Small Change Exception

Not every tiny repo action must traverse maximum ceremony.

A small bounded exception may exist for:

- trivial typo fixes
- tiny local safe corrections
- low-risk non-structural edits

But this exception must remain genuinely small.

It should not become a loophole that swallows normal branch/MR discipline.

### Principle

Exceptions should reduce friction without weakening the default controlled path.

---

## Health and Failure Signals

GitLab integration should make it easy to surface signals such as:

- CI failures
- MR blocked status
- repeated failed pipelines
- merge delay due to review or approval gates
- branch work that has stalled

These do not replace the global trace and reporting model,
but they are important operational inputs.

---

## Relation to Other Documents

This document should align with:

- `REPO_TEMPLATE_SPEC.md`
- `DEV_TASK_MODEL.md`
- `STATE_MACHINE.md`
- `RISK_MODEL.md`
- `APPROVAL_POLICY.md`
- `TRACE_SPEC.md`
- `CLAUDE_CODE_EXECUTION_SPEC.md`

This document defines GitLab integration posture.

It does not replace repo template, packet contracts, or approval/risk semantics.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- repo-centered work with no issue framing
- direct shared-surface changes without isolation
- MR bypass becoming normal
- CI being treated as optional
- merge happening without meaningful review posture
- GitLab existing as storage but not control
- workflow/config/governance changes being treated as ordinary low-risk edits
- executor output being too loose to fit governed repo flow

---

## Final Principle

GitLab should function as the durable development control surface around repo-centered work.

The correct integration makes change easier to isolate, easier to review, easier to validate, and safer to merge.

That is the point.