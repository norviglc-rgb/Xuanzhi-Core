# ROOT_FILE_POLICY.md

## Purpose

This document defines the write policy, scope boundaries, and change control rules for root-level standard files in the OpenClaw workspace.

Its goal is to keep the root workspace stable, short, high-signal, and compatible with OpenClaw's standard file injection model.

This policy exists to prevent:

- root file sprawl
- prompt bloat
- concept duplication
- governance drift
- accidental promotion of low-frequency detail into always-loaded context
- misuse of root files as long-form documentation storage

This document is normative for root-level standard files.

If another document suggests adding substantial detail to a root file, this policy takes precedence unless an explicit exception is approved and recorded.

---

## Design Principle

Root files are not general documentation.

Root files are the thin always-needed control surface of the workspace.

They exist to hold only the smallest set of rules and information that must be available at session start with high probability.

Everything else should default to one of these destinations:

- `governance/` for detailed governance specifications
- `contracts/` for machine-readable contracts and schemas
- `policies/` for machine-readable rules and policy tables
- `integrations/` for execution and external tool integration details
- `memory/` for daily memory and contextual records
- `workflows/` for execution flow assets and related implementation materials

Default rule:

When in doubt, do not add content to a root file.
Prefer downshifting the content into a lower layer.

---

## Scope

This policy applies to the following root-level files:

- `AGENTS.md`
- `SOUL.md`
- `USER.md`
- `IDENTITY.md`
- `TOOLS.md`
- `HEARTBEAT.md`
- `MEMORY.md`
- `BOOT.md`
- `BOOTSTRAP.md`

This policy does not directly govern lower-layer files under:

- `governance/`
- `contracts/`
- `policies/`
- `integrations/`
- `memory/`
- `workflows/`

However, it does govern when content should be moved from root files into those locations.

---

## Root File Role Model

### Root files are for high-frequency, high-stability, session-critical information

Content is eligible for a root file only if it is all of the following:

- high-frequency
- stable across many sessions
- short enough to remain legible and inexpensive
- important at session start
- inappropriate to rely on pure retrieval for every use

If any of the above is not clearly true, the content should not be promoted into a root file.

### Root files are not for complete detail

Root files must not become:

- full governance manuals
- long-form project archives
- registry field references
- complete workflow handbooks
- exhaustive tool documentation
- large knowledge base indexes
- historical logs
- execution traces
- long postmortems
- large prompt libraries

---

## Canonical Root File Responsibilities

### `AGENTS.md`

Purpose:

Defines the main agent operating contract.

Allowed content:

- the main role of the agent
- execution routing principles
- when to clarify
- when to escalate
- when to write memory
- when to hand off to a specialized executor
- high-level behavior rules

Disallowed content:

- complete state machine definitions
- full risk matrix
- complete trace schema
- registry field lists
- complete repo template details
- long workflow instructions
- per-integration operational playbooks
- detailed branching and CI policy tables

Guiding rule:

`AGENTS.md` should tell the agent how to operate at a high level, not contain the entire system manual.

### `SOUL.md`

Purpose:

Defines identity, values, tone, and non-negotiable persona boundaries.

Allowed content:

- who 玄织 is
- who 玄织 is not
- core values
- communication style
- core governance stance
- anti-role-drift boundaries

Disallowed content:

- procedural workflow instructions
- detailed approval logic
- tool routing tables
- implementation policy
- project-specific technical detail
- large examples

Guiding rule:

`SOUL.md` should shape character and stance, not act as a control handbook.

### `USER.md`

Purpose:

Defines stable user relationship and interaction boundaries.

Allowed content:

- user relationship stance
- confirmation rules for sensitive operations
- stable user preferences
- user-facing cooperation norms

Disallowed content:

- task history
- long-term work logs
- full project context
- large preference catalogs
- execution process detail
- detailed approval matrix
- system governance principles disguised as user preference

Guiding rule:

`USER.md` should hold durable interaction boundaries, not evolving task context or broad system doctrine.

### `IDENTITY.md`

Purpose:

Defines concise identity metadata.

Allowed content:

- name
- short role description
- concise positioning statement

Disallowed content:

- long persona definitions
- behavioral manuals
- tool policy
- workflow detail

Guiding rule:

`IDENTITY.md` should remain extremely short.

### `TOOLS.md`

Purpose:

Defines preferred tool usage posture and high-level routing guidance.

Allowed content:

- which tool classes are preferred for which task classes
- default executor statements
- high-level usage cautions
- concise output expectations
- tool selection guidance

Disallowed content:

- copied tool documentation
- full API specifications
- long argument references
- integration implementation guides
- detailed workflow DSL
- per-tool troubleshooting manuals
- broad governance philosophy unrelated to tool selection

Guiding rule:

`TOOLS.md` should explain how the workspace prefers to use tools, not document the tools completely or become a tool-governance manifesto.

### `HEARTBEAT.md`

Purpose:

Defines an extremely short operating checklist.

Allowed content:

- start-of-session reminders
- pre-response checks
- post-task summary checks
- minimal memory update reminders

Disallowed content:

- long procedures
- detailed review processes
- long escalation logic
- project history

Guiding rule:

`HEARTBEAT.md` should be tiny, mechanical, and stable.

### `MEMORY.md`

Purpose:

Defines long-term memory summary and navigation.

Allowed content:

- stable preferences
- major active initiatives
- durable decisions
- compact strategic memory
- navigation pointers to detail sources

Disallowed content:

- large daily logs
- detailed execution history
- full knowledge base catalogs
- full project document indexes
- large report bodies
- repetitive progress logs
- memory-writing policy explanations

Guiding rule:

`MEMORY.md` is an index and summary layer, not a dumping ground.

### `BOOT.md`

Purpose:

Defines a very short startup orientation.

Allowed content:

- what to read first
- how the workspace is layered
- where detailed specs live

Disallowed content:

- long training material
- full system handbook
- repeated content already present in root files

Guiding rule:

`BOOT.md` should help orientation, not duplicate the system.

### `BOOTSTRAP.md`

Purpose:

Defines one-time initialization guidance.

Allowed content:

- initial setup steps
- first-run questions
- initialization notes
- cleanup instructions after setup

Disallowed content:

- long-term operational policy
- evolving governance rules
- detailed technical playbooks

Guiding rule:

`BOOTSTRAP.md` should be temporary and disposable.

---

## Default Downshift Rule

Any new governance or operational content must default to a lower layer unless it clearly qualifies for root-level presence.

Preferred destinations:

- terminology and cross-file semantics -> `governance/GOVERNANCE_GLOSSARY.md`
- field naming standards -> `governance/FIELD_CANON.md`
- state logic -> `governance/STATE_MACHINE.md`
- risk logic -> `governance/RISK_MODEL.md`
- trace detail -> `governance/TRACE_SPEC.md`
- write thresholds and memory rules -> `governance/MEMORY_WRITE_POLICY.md`
- structured object rules -> `contracts/*.json`
- decision rules and gates -> `policies/*.yaml`
- executor and system integration details -> `integrations/*.md`
- daily and historical notes -> `memory/*.md`

Default principle:

New detail should move downward, not upward.

---

## Root File Admission Test

Before adding any content to a root file, all of the following questions must be checked.

### Test 1: Session-Critical

Is this information likely to be needed at session start across many sessions?

If no, do not place it in a root file.

### Test 2: High-Frequency

Will this information materially shape behavior often enough to justify constant injection?

If no, do not place it in a root file.

### Test 3: Stability

Is this content stable enough that frequent edits are unlikely?

If no, do not place it in a root file.

### Test 4: Compactness

Can this content be expressed concisely without becoming vague or lossy?

If no, do not place it in a root file.

### Test 5: Non-Retrievability

Would relying on on-demand retrieval here materially harm performance or consistency?

If no, do not place it in a root file.

### Admission Rule

Content should be promoted to a root file only if the answer is effectively yes to all five tests.

If uncertainty remains, the content must be downshifted.

---

## Root File Budget Model

These budgets are internal engineering targets, not official OpenClaw hard limits.

Officially, OpenClaw injects standard workspace files into session context and truncates large injected files using bootstrap file limits. OpenClaw also explicitly advises keeping some root files short, especially `HEARTBEAT.md` and `BOOT.md`. Community practice similarly favors auditing workspace size and trimming large injected files.

Therefore this workspace uses three budget levels:

- Target
- Review
- Refactor

### Budget interpretation

#### Target

Healthy operating range.

A file in this range is likely thin enough to remain practical as an injected root-layer file.

#### Review

The file may still be acceptable, but must be reviewed for:

- duplication
- prose-heavy explanation
- layer pollution
- policy or schema detail that should move downward
- repeated concepts already stated elsewhere

#### Refactor

The default response is:

- downshift
- split by layer
- remove explanation
- compress signal
- eliminate duplication

Do not rely on prompt compression, truncation, or model goodwill as the primary fix.

### Recommended ranges

#### `AGENTS.md`

- Target: 300-700 tokens
- Review: 700-1100 tokens
- Refactor: >1100 tokens

#### `SOUL.md`

- Target: 180-400 tokens
- Review: 400-650 tokens
- Refactor: >650 tokens

#### `USER.md`

- Target: 120-280 tokens
- Review: 280-450 tokens
- Refactor: >450 tokens

#### `IDENTITY.md`

- Target: 40-120 tokens
- Review: 120-200 tokens
- Refactor: >200 tokens

#### `TOOLS.md`

- Target: 180-420 tokens
- Review: 420-700 tokens
- Refactor: >700 tokens

#### `HEARTBEAT.md`

- Target: 60-160 tokens
- Review: 160-250 tokens
- Refactor: >250 tokens

#### `MEMORY.md`

- Target: 180-500 tokens
- Review: 500-900 tokens
- Refactor: >900 tokens

#### `BOOT.md`

- Target: 80-180 tokens
- Review: 180-280 tokens
- Refactor: >280 tokens

#### `BOOTSTRAP.md`

- Target: 100-250 tokens
- Review: 250-450 tokens
- Refactor: >450 tokens

### Character-level backstop

Even when token estimates look acceptable, root files should still be audited at the character level.

As a practical backstop:

- files above approximately 5000 characters deserve review
- files above approximately 10000 characters should be treated as strong refactor candidates unless unusually well justified

This is a practical anti-bloat rule, not a replacement for judgment.

---

## Prohibited Root File Growth Patterns

The following patterns are considered root-layer anti-patterns.

### Anti-pattern 1: Full manual inflation

A root file grows into a multi-topic handbook.

### Anti-pattern 2: Duplicate detail spread

The same rule appears in root and lower-layer files with slightly different wording.

### Anti-pattern 3: History dumping

A root file becomes a running archive of events, decisions, or progress logs.

### Anti-pattern 4: Technical annex creep

A root file starts to absorb schema detail, API detail, implementation notes, or long examples.

### Anti-pattern 5: Retrieval avoidance

A root file is expanded simply to avoid using the retrieval layer.

### Anti-pattern 6: Prompt superstition

Content is added to a root file only because it feels safer to keep it always visible, without evidence that it truly needs constant presence.

---

## Root File Change Control

### Default change posture

Changes to root files are allowed, but expansion is not presumed beneficial.

Root files should be treated as narrow interfaces.

### Required justification for expansion

Any change that increases a root file's scope, length, or specificity must explicitly answer:

- Why must this be always available at session start?
- Why can this not live in `governance/`, `memory/`, `integrations/`, `contracts/`, or `policies/`?
- Which file specifically requires the addition?
- What lower-layer alternative was considered?
- Does this create duplication elsewhere?

If these questions are not answered convincingly, the change should be rejected.

### Default approval stance

For root file expansion:

- default stance = reject unless justified
- default alternative = downshift
- default fix for ambiguity = place in lower layer first

---

## Root File Refactoring Rule

When a root file becomes too long, too specific, or too unstable, the system should not attempt to preserve the shape by compression alone.

The first preferred action is structural refactoring:

- remove duplication
- extract details into lower-layer documents
- replace long lists with concise principles
- move procedural detail into `governance/` or `integrations/`
- move machine-oriented detail into `contracts/` or `policies/`

Compression without boundary correction is not sufficient.

---

## Relation to Retrieval Layer

Root files are not the same as the retrieval layer.

The existence of search and QMD-backed recall is a reason to keep root files smaller, not larger.

Detailed and lower-frequency material should be placed where it can be found on demand rather than injected by default.

Therefore:

- root files should remain thin
- lower layers should remain searchable
- retrieval should absorb detail pressure
- root files should not be used to bypass retrieval design

---

## Relation to Machine-Readable Constraints

Root files are primarily human-readable behavioral and governance surfaces.

They are not the preferred destination for strong executable constraints.

If a rule is structurally important enough to require enforcement, it should usually also be represented in one or more of the following:

- JSON Schema
- YAML policy
- validator logic
- state transition table

Root files may reference those constraints at a high level, but should not substitute for them.

---

## Operational Rule for the Main Agent

The main agent must not directly promote detailed content into root files merely because the content seems useful.

When considering any root-file change, the main agent must first evaluate:

- whether the content is truly session-critical
- whether the content belongs to a lower layer
- whether the change introduces duplication
- whether the change should instead trigger a contract or policy update

If uncertainty remains, the main agent should propose a lower-layer change rather than a root-layer expansion.

Default behavior:

propose downshift first

---

## Exception Handling

Exceptions are allowed only when all of the following are true:

- the content is essential at session start
- retrieval would be too slow or too unreliable for the use case
- the content is stable
- the content remains concise
- the content does not materially duplicate lower-layer detail

Any exception should be recorded with:

- rationale
- affected file
- expected persistence duration
- review date if temporary

Temporary exceptions should be actively revisited and removed if they stop justifying root-level presence.

---

## Compliance Signals

Healthy root layer signals:

- files remain short
- responsibilities remain distinct
- retrieval handles most detail
- lower layers grow more than root files
- policy and contract layers absorb enforcement logic

Unhealthy root layer signals:

- repeated truncation pressure
- frequent expansion of `AGENTS.md`
- root files used as documentation storage
- duplication between root and governance layers
- increasing ambiguity about where new content belongs

---

## Final Principle

Root files are governance interfaces, not storage surfaces.

If everything rises to the root, the root stops guiding and starts drowning.

The correct default is disciplined thinness.