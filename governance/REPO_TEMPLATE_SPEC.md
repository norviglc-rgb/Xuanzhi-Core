# REPO_TEMPLATE_SPEC.md

## Purpose

This document defines the repository template specification for the Xuanzhi workspace.

Its purpose is to provide a stable baseline for creating governed repositories that are:

- structurally legible
- development-friendly
- governance-compatible
- automation-ready
- reviewable
- evolvable

This document is normative for repository template semantics.

It is not a GitLab API manual.
It is not a CI implementation file.
It is not a full bootstrap script.

Its job is to define what a governed repo template should contain, what directory and governance expectations apply, and how repo structure relates to the control model.

---

## Core Principle

A repo template should reduce ambiguity, not merely create folders.

A good template should make it easier to answer:

- where code belongs
- where documentation belongs
- where governance files belong
- where tests belong
- where scripts belong
- where project-specific agents or workflows belong
- how the repo should enter review and merge flow

A bad template creates ceremony without control value.

Therefore this workspace prefers a template model that is:

- minimal by default
- extensible by need
- governance-aware
- project-type aware

---

## Supported Repository Types

This workspace recognizes the following canonical repository types:

- `software_project`
- `automation_project`
- `agent_project`
- `infra_project`
- `knowledge_project`
- `research_project`

These types are governance-facing categories used to shape template defaults and expectations.

### `software_project`

Primary purpose:

- application or service development
- library or module development
- implementation-heavy code work

Typical emphasis:

- `/src`
- `/tests`
- CI
- review and delivery flow

### `automation_project`

Primary purpose:

- workflow automation
- pipeline logic
- integration tasks
- schedulers or support automations

Typical emphasis:

- `/scripts`
- `/workflows`
- `/docs`
- operational governance

### `agent_project`

Primary purpose:

- agent logic
- agent-facing workflow design
- control-plane or executor-facing code and config

Typical emphasis:

- `/agents`
- `/workflows`
- `/tools`
- `/docs`
- governance alignment

### `infra_project`

Primary purpose:

- deployment, runtime, configuration, or environment management

Typical emphasis:

- `/scripts`
- config management
- CI and security discipline
- stronger risk posture

### `knowledge_project`

Primary purpose:

- structured documentation
- knowledge base organization
- governance materials
- memory or retrieval-ready content

Typical emphasis:

- `/docs`
- governance structure
- low code footprint
- change clarity

### `research_project`

Primary purpose:

- structured experiments
- analysis
- investigation
- decision-support outputs

Typical emphasis:

- `/docs`
- `/scripts`
- optional `/src`
- reproducibility and artifact traceability

---

## Default Directory Structure

Every governed repo should include the following default directories unless there is a strong reason not to:

- `/docs`
- `/src`
- `/tests`
- `/scripts`
- `/.governance`

### `/docs`

Purpose:

- human-readable project documentation
- architecture notes
- operational notes
- design summaries
- user or maintainer guidance

### `/src`

Purpose:

- primary implementation source
- production logic
- library or service code
- core execution code

### `/tests`

Purpose:

- automated tests
- validation helpers
- regression checks
- quality verification assets

### `/scripts`

Purpose:

- utility scripts
- maintenance scripts
- bounded local automation
- project operations support

### `/.governance`

Purpose:

- project-local governance files
- project-local policy overlays
- local conventions that should not pollute the root workspace
- repo-scoped operational control notes

### Directory rule

The default structure should be present where it improves clarity.

Empty directories should not be forced if they add no control value,
but omission should be intentional rather than accidental.

---

## Optional Directories

The following directories are optional and should be added only when the project actually benefits from them:

- `/agents`
- `/workflows`
- `/tools`

### `/agents`

Use when the repo contains:

- agent definitions
- agent-specific prompts or logic
- executor-facing or control-agent-specific code/assets

### `/workflows`

Use when the repo contains:

- workflow definitions
- reusable flow assets
- workflow-oriented pipeline logic
- low-code or structured orchestration materials

### `/tools`

Use when the repo contains:

- repo-local tools
- helper executables
- tooling wrappers
- task-specific utility packages

### Optional directory rule

Do not add optional directories by default merely because they are available.

They should exist only when they improve project legibility or execution fit.

---

## Governance File Placement

Project-level governance files should live under:

- `/.governance`

rather than polluting the main workspace root or scattering across arbitrary locations.

Typical project-local governance content may include:

- project-local operating notes
- local approval overlays
- project-local risk notes
- project-local conventions
- project-local delivery or review checklists

### Placement rule

Repo-local governance belongs to the repo.
Workspace-wide governance belongs to the main Xuanzhi workspace.

Do not confuse the two layers.

---

## Template and Root-Workspace Relation

The repo template is not the same thing as the main OpenClaw workspace root.

The main workspace root defines:

- Xuanzhi top-layer control behavior
- workspace-level governance
- workspace-level memory and contracts

A repo template defines:

- project-level structure
- project-local development surfaces
- project-local governance placement
- project-local CI and issue expectations

### Principle

A governed repo should be compatible with the main workspace,
but it should not blindly duplicate the entire workspace root layer.

---

## Issue Template Baseline

Every governed repo should support at least the following issue categories:

- `feature`
- `bug`
- `task`
- `research`
- `governance`

These categories are intentionally small.

### `feature`

Use for new capability work.

### `bug`

Use for defects, regressions, or incorrect behavior.

### `task`

Use for bounded implementation or maintenance work not best described as feature or bug.

### `research`

Use for investigation, comparison, uncertainty reduction, or exploratory decision support.

### `governance`

Use for policy, structure, workflow, review, or control-related changes.

### Issue baseline rule

Issue taxonomy should stay small unless real volume proves the need for more categories.

Do not create category inflation early.

---

## Branch Naming Baseline

The default branch families are:

- `feature/*`
- `fix/*`
- `research/*`
- `infra/*`
- `experiment/*`

### Meaning

- `feature/*` -> new capability work
- `fix/*` -> bug or correction work
- `research/*` -> investigation or analysis work
- `infra/*` -> infrastructure, deployment, or operational work
- `experiment/*` -> bounded experimental work not yet treated as stable product direction

### Branch rule

Branch naming should communicate work intent.

Do not create arbitrary branch naming schemes when a simple canonical set is sufficient.

---

## CI Baseline

Default CI checks should include:

- lint
- test
- build
- security scan

### CI rule

CI failure should block merge by default.

This is a governance baseline, not an optional decoration.

### Why

The point is not perfection theater.

The point is to preserve:

- review quality
- merge discipline
- delivery confidence
- recoverability

### Flexibility rule

The exact CI implementation may vary by project type,
but the baseline expectation should remain.

---

## Merge and Review Baseline

Governed repos should support a merge flow consistent with:

`Issue -> Branch -> MR -> CI -> Review -> Merge`

This should be treated as the default controlled path.

### Review posture

Review may be performed by:

- dedicated review agents
- dedicated delivery review agents
- humans when risk, ambiguity, or repeated failure justify escalation

### Principle

The repo template should make this path easier, not harder.

---

## Automatic Repository Creation

Xuanzhi may be allowed to create repos automatically where policy permits.

### Automatic creation should still preserve:

- repo type selection
- directory structure fit
- governance placement
- issue template baseline
- branch naming baseline
- CI baseline

Automatic creation should not mean ungoverned creation.

---

## Repository-Type Guidance

### `software_project` recommended layout

Strongly expected:

- `/src`
- `/tests`
- `/docs`
- `/scripts`
- `/.governance`

Optional:

- `/tools`

### `automation_project` recommended layout

Strongly expected:

- `/scripts`
- `/docs`
- `/.governance`

Often useful:

- `/workflows`
- `/tools`

### `agent_project` recommended layout

Strongly expected:

- `/docs`
- `/.governance`

Often useful:

- `/agents`
- `/workflows`
- `/tools`
- `/src`
- `/tests`

### `infra_project` recommended layout

Strongly expected:

- `/scripts`
- `/docs`
- `/.governance`

Often useful:

- `/tests`
- `/tools`

### `knowledge_project` recommended layout

Strongly expected:

- `/docs`
- `/.governance`

Optional:

- `/scripts`

### `research_project` recommended layout

Strongly expected:

- `/docs`
- `/.governance`

Often useful:

- `/scripts`
- `/src`
- `/tests`

### Type guidance rule

Project type should bias the template,
but should not force obviously unnecessary folders.

---

## Minimal Project Files

A governed repo will often benefit from a small set of baseline files.

Typical examples may include:

- `README.md`
- `.gitignore`
- CI config
- issue templates
- MR template
- selected project-local governance files under `/.governance`

This document does not freeze the exact contents of every baseline file,
but it does define that baseline project structure should make collaboration and governance easier from day one.

---

## Project-Local Governance Baseline

The `/.governance` directory may contain files such as:

- project-specific working agreements
- local review notes
- risk notes
- delivery notes
- repo-local memory or navigation docs
- local policy overlays

### Important rule

Project-local governance should remain repo-relevant.

Do not replicate the full workspace governance stack inside every repo.

Only store the minimum repo-local governance that improves project control.

---

## Repository Template and Development Executor Fit

The repo template should support the current bounded executor strategy.

### For Claude Code

The repo should be easy to navigate for long-running development execution, including:

- clear code location
- clear test location
- clear scripts location
- clear docs location
- obvious governance location

### For Xuanzhi

The repo should make it easy to:

- review repo purpose
- understand project type
- identify governance-relevant files
- summarize status
- route development tasks

### Principle

Repo structure should help both execution and governance.

---

## Repository Template and Traceability

The repo template should support future traceability indirectly by making it easier to:

- locate changed files
- identify relevant docs
- separate source from scripts
- separate governance from implementation
- connect MR and CI review to project structure

The template should not become a trace system itself.
It should support traceability through legible structure.

---

## Repository Template and Risk

Some repo types naturally tend toward higher-risk surfaces.

Examples:

- `infra_project`
- runtime-sensitive automation repos
- repos containing deployment or control-plane logic

These repos may require stronger project-local review or policy overlays under `/.governance`,
but this document does not force every repo template into a high-risk governance footprint.

### Principle

Template should adapt to real project risk,
not impose maximum ceremony everywhere.

---

## Relation to Other Documents

This document should align with:

- `DEV_TASK_MODEL.md`
- `RISK_MODEL.md`
- `AGENT_REGISTRY_SPEC.md`
- `WORKFLOW_REGISTRY_SPEC.md`
- future GitLab integration and approval policy specs

This document defines repository template semantics.

Later automation or bootstrap specifications may define how these templates are instantiated.

---

## Failure Modes This Specification Should Prevent

This specification exists partly to prevent:

- repo sprawl without structure
- code and governance files being mixed arbitrarily
- templates that are too empty to govern
- templates that are too ceremonial to use
- project-type confusion
- branch and issue chaos
- CI being treated as optional decoration
- local repo governance leaking into the wrong layer

---

## Final Principle

A good repo template should make the right work easier.

It should not exist merely to look organized.

The correct template is the one that makes development, review, and governance more legible with the least necessary ceremony.