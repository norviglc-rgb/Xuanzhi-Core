# MEMORY.md

## Purpose

This file stores curated long-term memory for the 玄织 workspace.

It is a summary-and-navigation layer.

Its job is to preserve durable context that should shape future judgment across sessions.

It is not:

- a full project archive
- a task tracker
- a running execution log
- a daily notebook
- a full knowledge base catalog
- a place for large copied materials

Detailed or short-lived notes belong in `memory/YYYY-MM-DD.md` or other lower-layer documents.

---

## Memory Posture

Memory should be:

- durable
- useful across sessions
- low-noise
- summary-oriented
- selective
- easy to reuse
- easy to review

Memory should not become a trash heap of temporary context.

A smaller and cleaner memory is usually more useful than a larger and noisier one.

---

## What Belongs Here

This file should preserve only information that is likely to matter again beyond the current moment.

Appropriate content includes:

- stable user collaboration preferences
- stable system-shape decisions
- active major initiatives at summary level
- durable architectural decisions
- major governance constraints
- major executor-boundary decisions
- important lessons worth reusing
- navigation pointers to deeper detail

---

## What Does Not Belong Here

The following should normally not be stored here:

- temporary task state
- verbose daily progress
- full conversation transcripts
- long reasoning chains
- full change histories
- copied source documents
- repetitive meeting-style notes
- detailed implementation logs
- short-lived reminders
- large lists of minor facts
- operational noise

If a piece of information is likely to expire soon, it probably does not belong here.

If a piece of information is only useful for one active thread, it probably belongs in a daily note rather than long-term memory.

---

## Memory Categories

### 1. Stable Preferences

Use this section for durable collaboration preferences that repeatedly improve future interaction.

Examples:

- preference for critical and first-principles reasoning
- preference for thin root files
- preference for pushing detail downward into retrieval layers
- preference for governance clarity over decorative complexity

Only stable preferences should appear here.

### 2. System Shape Decisions

Use this section for durable architectural choices about how the system is organized.

Examples:

- 玄织 is the governance core
- OpenClaw is the main control-plane workspace
- Claude Code is the default development executor
- long-running development stays in Claude Code rather than the OpenClaw top layer
- workflow and media execution may be delegated to specialized systems

These are memory-worthy because they affect many later decisions.

### 3. Active Strategic Focus

Use this section for major ongoing directions at a summary level.

This section should remain compact.

It may include:

- the current main design direction
- active architecture cleanup focus
- current implementation phase at a high level

It should not become a running backlog or detailed roadmap.

### 4. Durable Lessons

Use this section for lessons that were learned through repeated friction, failure, or design review and are likely to remain useful later.

Examples:

- root-layer prompt inflation is a real risk
- prose-only governance leads to soft control
- retrieval should absorb detail pressure
- heavy execution should be delegated downward

Lessons should be phrased compactly and generally enough to reuse.

### 5. Navigation Pointers

Use this section to point toward deeper sources.

Examples:

- detailed governance specs live in `governance/`
- machine-readable contracts live in `contracts/`
- machine-readable rules live in `policies/`
- executor and workflow details live in `integrations/` and `workflows/`
- daily notes live in `memory/YYYY-MM-DD.md`

Pointers are useful.
Large embedded detail is not.

---

## Memory Writing Rule

Before writing to this file, 玄织 should check:

- is this durable across sessions
- will this likely matter again
- is this summary-level rather than process-level
- is this better stored here than in `memory/YYYY-MM-DD.md`
- will adding this make retrieval clearer rather than noisier

If the answer is uncertain, the default action is not to write here.

The default action is to keep the information in a lower or more temporary layer.

---

## Memory Editing Rule

When editing this file, prefer:

- condensation over accumulation
- replacement over duplication
- summary over detail
- category clarity over chronological sprawl

This file should become more legible over time, not merely longer.

If a section grows too large, it should be split by meaning or downshifted into another file with only a short pointer retained here.

---

## Current Stable Preferences

- The user prefers critical, first-principles, anti-drift reasoning.
- The user prefers a strong first version with clean structural bones.
- The user prefers root-layer files to remain thin.
- The user prefers detailed rules to move downward into retrieval layers rather than inflate prompt context.
- The user prefers important rules to be hardened into schema, policy, validator logic, or state tables when appropriate.
- The user prefers disciplined cooperation rather than obedience theater.

---

## Current System Shape Decisions

- 玄织 is the governance core and top-layer control surface.
- OpenClaw is the main workspace for intake, routing, summary, memory discipline, and reporting.
- Claude Code is the default executor for long-running development work.
- FastGPT and other workflow systems may be used for suitable workflow-facing tasks, but they do not replace top-layer governance.
- Specialized media or automation systems may perform narrow execution and report upward.
- The workspace should grow downward before it grows outward.
- Root files should remain narrow, stable, and session-critical.

---

## Current Active Strategic Focus

- Build an OpenClaw-compatible first-version workspace with a thin root layer.
- Move long governance detail into searchable lower layers.
- Establish strong anti-drift policies before expanding the file set.
- Create a stable interface between 玄织 and Claude Code for long-running development.
- Gradually convert critical governance rules from prose-only form into machine-readable constraints.

---

## Current Durable Lessons

- Prompt safety is not the same as control; important rules eventually need hardening.
- A detailed Markdown governance layer without contracts and policies will drift.
- Root files degrade when they become storage surfaces instead of control surfaces.
- Delegation improves stability when heavy execution is pushed to the correct executor.
- Retrieval is a core design tool, not a fallback for missing discipline.
- Phase review is necessary because drift often appears as “reasonable additions.”

---

## Navigation Pointers

- Root-layer behavior and identity live in:
  - `AGENTS.md`
  - `SOUL.md`
  - `USER.md`
  - `IDENTITY.md`
  - `TOOLS.md`
  - `HEARTBEAT.md`
  - `BOOT.md`

- Detailed governance specifications live in:
  - `governance/`

- Machine-readable contracts live in:
  - `contracts/`

- Machine-readable policy artifacts live in:
  - `policies/`

- Integration and executor-specific documents live in:
  - `integrations/`

- Workflow assets and pipeline materials live in:
  - `workflows/`

- Daily or temporary notes live in:
  - `memory/YYYY-MM-DD.md`

---

## Final Principle

This file should help future sessions recover the shape of the system quickly.

If it becomes noisy, oversized, or over-detailed, it has failed.

Long-term memory should sharpen judgment, not blur it.