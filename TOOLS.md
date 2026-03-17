# TOOLS.md

## Purpose

This file defines the preferred tool-use posture of the 玄织 workspace.

It is a root-layer routing aid.

It does not replace official tool documentation.
It does not contain detailed integration manuals.

---

## Core Rule

Use the simplest tool or executor that fits the real task.

Do not centralize heavy execution at the top layer when a lower-layer executor is clearly a better fit.

Do not inflate root-layer context with detailed tool explanations.

---

## Preferred Roles

### 玄织 / OpenClaw main agent

Use for:

- intake
- routing
- summary
- governance judgment
- light analysis
- reporting
- memory discipline
- retrieval-guided responses without heavy execution

### Claude Code

Default development executor.

Use for:

- long-running software development
- repository changes
- implementation-heavy tasks
- iterative coding and testing
- structured development execution

### FastGPT or other workflow systems

Use for:

- workflow-facing tasks
- low-code or user-facing process flows
- lightweight structured execution
- some information collection or dispatch tasks

### Specialized external systems

Use for:

- media generation
- integration-heavy pipelines
- narrow specialized execution
- tasks better handled by dedicated external services

---

## Routing Preference

Route to 玄织 when the task is mainly:

- interpretive
- governance-related
- summary or review oriented
- planning or routing oriented
- retrieval-guided without heavy execution

Route to Claude Code when the task is mainly:

- development-heavy
- repository-centered
- long-running
- implementation-focused
- iterative software delivery work

Route to workflow or specialized systems when the task is mainly:

- repetitive
- pipeline-like
- media-generation oriented
- integration-heavy
- better served by an existing execution system

---

## Retrieval Rule

If information is detailed, long, or specialized, prefer retrieval over expanding root files.

Detailed governance, integration, historical, or reference material should usually be found on demand rather than kept in always-loaded root files.

---

## Delegation Rule

Delegation is normal.

玄织 should retain:

- framing
- routing
- review posture
- summary
- memory discipline
- governance judgment

Heavy execution should move downward when that improves fit, quality, or context efficiency.

---

## Output Preference

When tools or executors are used, prefer outputs that are:

- concise
- structured
- reviewable
- easy to summarize
- easy to reference later

Prefer summaries and artifact references over large raw output.

---

## Boundary Reminder

This file should not absorb:

- full API references
- detailed executor manuals
- installation procedures
- troubleshooting guides
- workflow implementation detail
- broad governance doctrine unrelated to tool use

Those belong in lower layers.

---

## Final Principle

Choose the executor that matches the work.

Keep the top layer thin.
Delegate heavy execution downward.
Use retrieval for detail.
Retain governance at the center.