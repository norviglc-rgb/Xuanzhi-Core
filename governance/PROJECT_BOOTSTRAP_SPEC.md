# PROJECT_BOOTSTRAP_SPEC.md

## Purpose

This document defines the project bootstrap specification for the Xuanzhi workspace.

Its purpose is to provide a stable governed path from:

- project intent
- task framing
- repository creation or selection
- template selection
- initial governance setup
- development handoff readiness

This document is normative for project bootstrap semantics.

It is not a shell script.
It is not a GitLab API reference.
It is not a repo template file itself.
It is not a substitute for development task packets or project-local governance files.

Its job is to define how a new project should enter the governed system.

---

## Core Principle

Project bootstrap is not merely “create repo and start coding.”

A governed bootstrap should answer:

- what kind of project this is
- why the project exists
- what repo shape it should have
- what governance baseline applies
- what the initial execution posture is
- what the first controlled development path is

A bad bootstrap creates infrastructure without clarity.

This workspace prefers bootstrap that is:

- minimal
- explicit
- type-aware
- governance-compatible
- ready for bounded execution

---

## Bootstrap Entry Conditions

Bootstrap begins when a project-level effort is recognized that needs one or more of the following:

- a new repository
- a new governed project space
- a new project-local governance surface
- a new long-running development track
- a new workflow-bearing or automation-bearing project unit

Not every task requires project bootstrap.

Small bounded work inside an existing healthy repo should not be forced into new-project ceremony.

---

## Bootstrap Output Goal

A successful bootstrap should produce a project that is:

- clearly classified
- clearly owned
- structurally legible
- compatible with the workspace governance model
- ready for controlled development or workflow execution
- reviewable as a project entry point

At minimum, a successful bootstrap should make the next development decision easier and safer.

---

## Canonical Bootstrap Phases

The canonical project bootstrap phases are:

1. project framing
2. project type selection
3. repository strategy decision
4. template application
5. project-local governance baseline
6. initial issue/task setup
7. execution readiness check

These phases should remain conceptually distinct even if implementation later compresses them.

---

## Phase 1: Project Framing

Project framing should answer the minimum essential questions:

- what problem or objective does the project address
- what kind of work does the project mainly involve
- what is the expected first deliverable
- what is the likely primary executor
- what risk posture should be assumed initially

### Framing outputs

Useful outputs include:

- project summary
- project type candidate
- expected deliverable class
- initial repo need judgment
- likely executor posture

### Principle

If the project cannot be framed, repo creation should not be the first action.

---

## Phase 2: Project Type Selection

The project should be classified using the canonical repository types:

- `software_project`
- `automation_project`
- `agent_project`
- `infra_project`
- `knowledge_project`
- `research_project`

### Why type selection matters

Project type influences:

- template shape
- optional directories
- CI expectations
- local governance burden
- likely executor fit
- likely review posture

### Selection rule

Use the narrowest project type that fits the real work.

Do not choose a more complex type merely because it sounds more advanced.

---

## Phase 3: Repository Strategy Decision

The bootstrap path must decide whether to:

- use an existing repo
- create a new repo
- defer repo creation temporarily

### Use an existing repo when

- the work clearly belongs to an existing healthy project surface
- repo-local governance already exists
- creating a new repo would create duplication
- the existing repo structure still fits the work

### Create a new repo when

- the project is genuinely distinct
- ownership or lifecycle should be separate
- existing repos would create structural confusion
- the project type or control surface is materially different
- a clean governance boundary is valuable

### Defer repo creation when

- framing is still too unclear
- the work is exploratory and not yet project-shaped
- a small research or design phase should happen first

### Principle

A new repo is a governance decision, not merely a storage convenience.

---

## Phase 4: Template Application

If a new repo is created, it should apply the relevant template baseline from:

- `REPO_TEMPLATE_SPEC.md`

### Template application should include

- required default directories
- optional directories only when justified
- baseline project files
- CI baseline posture
- issue category baseline
- branch naming baseline
- project-local governance placement under `/.governance`

### Principle

Template application should reduce future ambiguity, not create decorative structure.

---

## Phase 5: Project-Local Governance Baseline

A new governed repo should gain a minimal project-local governance baseline.

This should live under:

- `/.governance`

### Project-local governance should be minimal

Typical bootstrap-level project-local governance may include:

- local project summary
- local conventions if needed
- local delivery notes if needed
- local risk notes if needed
- references to workspace-level governance

### Important rule

Do not duplicate the full workspace governance stack inside each repo.

The project-local governance baseline should remain project-specific and minimal.

---

## Phase 6: Initial Issue / Task Setup

Bootstrap should create a bounded first work surface.

This usually means at least one of:

- an initial issue
- an initial development task
- an initial research task
- an initial governance/setup task

### Why this matters

Bootstrap should not end with an empty repo plus vague hope.

It should end with a first controlled path.

### Typical initial issue examples

- initialize baseline project structure
- implement first bounded feature slice
- set up CI baseline
- create first automation skeleton
- establish initial docs and validation posture

---

## Phase 7: Execution Readiness Check

Before active development starts, the project should pass a lightweight readiness check.

### Minimum readiness questions

- is the project type clear enough
- is the repo choice correct enough
- is the structure legible enough
- is the initial task clear enough
- is the likely executor clear enough
- is the governance baseline sufficient for first work
- is the risk posture acceptable for bootstrap scope

### Principle

Readiness should be enough to start well,
not a giant pre-execution bureaucracy.

---

## Expected Bootstrap Artifacts

A healthy bootstrap often produces artifacts such as:

- project summary
- selected project type
- repo reference
- template application result
- local governance baseline under `/.governance`
- initial issue or task
- initial executor recommendation
- initial risk posture summary

These artifacts do not need to be large.

They do need to be legible.

---

## Executor Fit During Bootstrap

Bootstrap should preserve the existing bounded executor model.

### Xuanzhi

Xuanzhi is responsible for:

- framing the project
- selecting the project type
- deciding repo strategy
- determining initial governance posture
- deciding whether work is ready for development delegation

### Claude Code

Claude Code may become the default executor after bootstrap when the project is development-heavy and repo-centered.

### Workflow systems

Workflow systems may be suitable for bootstrap-adjacent automation work,
but should not replace project framing and governance judgment.

### Principle

Bootstrap is governance-first, execution-second.

---

## Risk and Approval During Bootstrap

Bootstrap can look administrative while still carrying real risk.

Approval or stronger scrutiny may be appropriate when bootstrap includes:

- repo creation in sensitive org surfaces
- infra project creation
- workflow-bearing project creation with activation implications
- permission-bearing setup
- risky project-local governance changes
- automation project creation with meaningful blast radius

### Principle

Bootstrap is not automatically low-risk just because it happens “before real work.”

---

## Repo Reuse vs Repo Proliferation

One of the most important bootstrap decisions is whether a new repo is actually justified.

### Signs that a new repo is justified

- distinct ownership
- distinct lifecycle
- distinct project type
- strong structural separation value
- reduced future confusion

### Signs that a new repo is probably not justified

- the work is just one bounded feature inside an existing repo
- repo separation adds ceremony but not control
- ownership and lifecycle are not materially different
- the new repo would mostly duplicate existing structure

### Principle

Avoid repo proliferation without governance value.

---

## Bootstrap and Development Packets

Bootstrap should make later development packet generation easier.

A good bootstrap should leave the project in a state where Xuanzhi can later produce clean:

- `dev_task_packet.schema.json` inputs
- `dev_result_packet.schema.json` review expectations

### Principle

Bootstrap is partly successful when the first development delegation becomes easier and cleaner.

---

## Bootstrap and GitLab

When GitLab is the repo control surface, bootstrap should support:

- governed repo creation
- issue-driven first work
- branch-aware future development
- MR/CI-ready structure

This should align with:

- `GITLAB_INTEGRATION.md`

---

## Bootstrap and Trace

Meaningful bootstrap actions should be traceable.

Typical bootstrap trace-worthy moments include:

- project framing accepted
- repo creation
- template applied
- initial governance baseline created
- initial issue or task opened
- first executor recommendation established

Bootstrap should not be invisible if it creates durable project structure.

---

## Bootstrap and Memory

Not every bootstrap event belongs in long-term memory.

However, memory-worthy bootstrap outcomes may include:

- durable project direction
- major architectural project classification
- important structural decisions about repo or project boundaries

Trace and repo artifacts should hold most bootstrap detail.
Long-term memory should hold only durable strategic signal.

---

## Small Bootstrap Exception

Not every new workstream needs full bootstrap.

A very small bounded project-like effort may use a light bootstrap path if:

- the project is obviously simple
- the risk is low
- the repo shape is trivial
- the initial work is clear
- future governance burden is low

### Principle

A light bootstrap is acceptable when it preserves clarity without unnecessary ceremony.

It should not become an excuse for structural sloppiness.

---

## Relation to Other Documents

This document should align with:

- `REPO_TEMPLATE_SPEC.md`
- `CLAUDE_CODE_EXECUTION_SPEC.md`
- `GITLAB_INTEGRATION.md`
- `CONTROLLER_API_SPEC.md`
- `DEV_TASK_MODEL.md`
- `RISK_MODEL.md`
- `APPROVAL_POLICY.md`

This document defines bootstrap semantics.

It does not replace repo template, controller packet, or execution integration specifications.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- repo creation without framing
- empty governed repos with no first work path
- project sprawl without structural justification
- project-local governance duplication
- bootstrap that creates folders but not clarity
- early executor selection without project shape understanding
- treating project bootstrap as trivial administration

---

## Final Principle

A good bootstrap creates a project that is easier to govern, easier to develop, and easier to review from the first meaningful step.

That is the point.