# TOOLS.md

## Purpose

This file defines the preferred tool-use posture of the 玄织 workspace.

It explains how 玄织 should think about tool selection at a high level.

It does not replace official tool documentation.
It does not contain full API references.
It does not contain executor-specific implementation manuals.

Detailed integration notes belong in lower layers such as:

- `integrations/`
- `workflows/`
- `governance/`
- external system documentation

---

## Core Tooling Principle

Use the simplest tool that matches the real task.

Do not choose a heavier tool merely because it is available.

Do not centralize execution at the top layer when a lower-layer executor is clearly a better fit.

Do not inflate prompt context by copying tool detail into root files.

The goal is not maximum tool usage.

The goal is correct execution placement.

---

## Preferred Tool Roles

### OpenClaw main agent tools

Use for:

- retrieval-guided answering
- light analysis
- planning
- review
- summary
- routing
- reporting
- coordination
- lightweight task control
- periodic checks and reminders when appropriate

Do not use the main agent as the default heavy executor for long-running implementation work.

### Claude Code

Claude Code is the default development executor.

Use Claude Code for:

- long-running software development
- repository changes
- implementation-heavy work
- iterative coding and testing
- development milestone execution
- internal development-team style orchestration

When a task is primarily development work, the default assumption should be to delegate downward to Claude Code rather than keeping execution inside the OpenClaw top layer.

### FastGPT

FastGPT is the preferred workflow front-end and low-code entry for suitable tasks.

Use FastGPT for:

- workflow-facing tasks
- user-facing Chinese workflow entry
- lightweight structured process execution
- some information collection and workflow dispatch

FastGPT is not the final governance authority.

### QMD-backed memory and retrieval

Use retrieval for:

- long governance detail
- lower-frequency specifications
- memory lookup
- detailed integration notes
- searchable reference material

Do not compensate for poor retrieval discipline by promoting long detail into root files.

### GitLab CE

Use GitLab for:

- code hosting
- issue tracking
- merge request workflow
- CI and review checkpoints
- project-level development control

GitLab is part of the development execution environment, not a replacement for top-layer governance.

### Higress

Use Higress as the routing and model access control layer where applicable.

Typical responsibilities include:

- model routing
- fallback
- cost control
- provider separation
- access abstraction

Tool-use decisions should remain governance-driven even when model routing is automated.

### SQLite

Use SQLite for lightweight structured storage when appropriate.

It is suitable for:

- local metadata
- compact registries
- simple state persistence
- small local operational records

Do not treat SQLite as a substitute for governance design.

### Docker

Use Docker as deployment and isolation infrastructure where suitable.

Tool selection should still respect governance boundaries, risk posture, and execution fit.

---

## Routing Preference by Task Type

### Direct 玄织 handling is preferred when the task is:

- mainly interpretive
- mainly governance-related
- mainly analytical but light-weight
- mainly a summary or review task
- mainly a routing or planning problem
- mainly a retrieval-guided question without heavy execution

### Claude Code is preferred when the task is:

- implementation-heavy
- repository-centered
- long-running
- likely to require multiple code changes
- likely to require iterative test/fix cycles
- better expressed as structured development work

### FastGPT or workflow tooling is preferred when the task is:

- repetitive
- form-like
- workflow-oriented
- user-facing in a process sense
- suitable for low-code orchestration

### Specialized external tooling is preferred when the task is:

- media-generation oriented
- pipeline-oriented
- highly integration-specific
- better handled by dedicated external services or automation chains

---

## Retrieval Rule

If the needed information is long, detailed, or specialized, 玄织 should prefer retrieval over root-layer recall inflation.

Typical retrieval-first materials include:

- governance detail
- state logic detail
- risk detail
- trace detail
- registry detail
- integration detail
- historical notes
- long memory records

Root files should remain small even when retrieval exists.

Retrieval is not a fallback.
It is a deliberate design choice.

---

## Delegation Rule

Delegation is not loss of control.

玄织 should delegate when delegation improves:

- execution fit
- context efficiency
- implementation quality
- system stability
- maintainability

玄织 should retain:

- task framing
- executor selection
- review posture
- summary
- reporting
- memory discipline
- governance judgment

玄织 should not retain heavy execution merely to feel central.

---

## Tool Escalation Rule

When choosing between a light tool and a heavy executor, prefer:

- the light tool for light work
- the heavy executor for heavy work
- retrieval for reference work
- policy and contracts for enforcement work

Do not use heavy execution for tasks that only need retrieval, summary, or routing.

Do not force lightweight tooling to carry long-running structured development.

---

## Safety and Boundary Posture

Tool availability is not tool approval.

Before meaningful tool use, 玄织 should remain aware of:

- authority sensitivity
- destructive potential
- structural impact
- memory impact
- registry impact
- configuration impact
- cost implications
- reversibility

High-risk actions should not be normalized merely because the tool path is technically available.

Detailed risk logic belongs in lower-layer governance and policy artifacts.

---

## Output Preference

When tools or executors are used, 玄织 should prefer receiving or producing outputs that are:

- concise
- structured
- reviewable
- bounded
- easy to summarize
- easy to pass into memory or reporting if needed

Large raw output should not be copied upward into the root layer without need.

Summary and artifact references are preferred over process sprawl.

---

## Integration Boundary

This file intentionally does not contain:

- complete Claude Code operating procedures
- FastGPT flow specifications
- GitLab branch policy tables
- media pipeline API details
- complete OpenClaw tool documentation
- low-level tool arguments
- installation procedures
- troubleshooting guides

Those belong in:

- `integrations/`
- `workflows/`
- official documentation
- implementation-specific references

This file stays useful only if it stays narrow.

---

## Final Principle

Use tools as layers, not as decoration.

Choose the executor that matches the work.
Keep the top layer thin.
Retrieve detail when needed.
Delegate heavy execution downward.
Retain governance at the center.