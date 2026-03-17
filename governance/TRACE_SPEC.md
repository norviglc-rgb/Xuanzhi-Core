# TRACE_SPEC.md

## Purpose

This document defines the trace model of the Xuanzhi workspace.

Its purpose is to provide a stable baseline for:

- auditability
- recovery support
- reviewability
- reporting support
- long-running task supervision
- governance accountability

This document is normative for trace semantics.

It is not a full log-ingestion design.
It is not a substitute for runtime observability tooling.
It is not a request to record everything.

Its job is to define what should be traced, how trace should be shaped, and what trace is not.

---

## Core Principle

Trace exists to preserve accountable signal.

Trace should help answer questions such as:

- what happened
- why it happened
- who initiated it
- who executed it
- what changed
- what risk posture applied
- what review or approval state mattered
- what the next recovery or continuation point is

A bad trace system records too much noise, too little structure, or the wrong kind of detail.

This workspace prefers:

- structured trace over narrative dump
- summaries over raw process sprawl
- references over payload duplication
- accountability over verbosity

---

## Trace Is Not

Trace is not:

- full chain-of-thought storage
- full transcript storage
- raw reasoning dump
- a substitute for memory
- a substitute for governance specs
- a substitute for runtime metrics tooling
- a place to copy large artifacts inline

Trace should preserve decision-relevant and audit-relevant signal,
not every intermediate thought or every large payload.

---

## Trace Domains

This workspace recognizes the following trace domains:

- task trace
- step trace
- review trace
- approval trace
- agent trace
- tool/workflow trace
- memory trace
- alert trace

These domains may share common fields,
but they serve different accountability purposes.

---

## Common Trace Identity

All trace-like records should prefer the following identity and linkage fields where applicable:

- `trace_id`
- `task_id`
- `step_id`
- `parent_trace_id`
- `parent_task_id`
- `epic_id`
- `milestone_id`

Not every trace record requires every linkage field.

The principle is:

include the minimum fields needed to preserve useful traceability

---

## Common Trace Responsibility Fields

Where applicable, trace records should preserve:

- `initiator`
- `executor`
- `approver`

### Definitions

#### `initiator`
The actor that originated the request, trigger, or step.

#### `executor`
The actor or system that actually performed the action.

#### `approver`
The actor or authority that granted or denied approval when approval matters.

These fields improve auditability and reduce blame ambiguity.

---

## Common Trace Content Fields

The following fields are preferred for structured trace records where relevant:

- `summary`
- `reasoning_summary`
- `status_summary`
- `risk_level`
- `review_state`
- `approval_state`
- `artifact_refs`
- `created_at`

### `summary`
Compact description of what happened.

### `reasoning_summary`
Compact explanation of why a path or decision existed.

Must remain summary-level.
Must not become raw chain-of-thought.

### `status_summary`
Compact statement of current result or current condition.

### `artifact_refs`
References to outputs, commits, files, or generated artifacts instead of inlining all content.

---

## Task Trace

Task trace records major task-level events and transitions.

Typical task trace moments include:

- task created
- task delegated
- task enters running state
- task enters waiting state
- task is replanned
- task is escalated
- task is completed
- task fails
- task is cancelled

### Task trace should answer

- what happened to the task
- why its state changed
- what executor path was chosen
- what major blockers or risks were present
- what the next governance-relevant checkpoint is

Task trace should remain summary-oriented, not step-by-step narration of everything.

---

## Step Trace

Step trace records bounded execution or decision steps.

Typical step trace moments include:

- step created
- step started
- step completed
- step failed
- step retried
- step replanned
- step blocked
- step cancelled

### Step trace should capture

- what step was attempted
- what action category or action name was involved
- whether the step succeeded
- what output or artifact references were produced
- what risk posture applied
- what next decision is likely

If the step object already contains detailed bounded context, trace should summarize and reference rather than duplicate.

---

## Review Trace

Review trace records the evaluation of outputs and delivery checkpoints.

Typical review trace moments include:

- review requested
- review started
- review passed
- review failed
- review conflicted

### Review trace should capture

- what was reviewed
- what standard or expectation applied
- what the outcome was
- whether blockers or major findings exist
- whether continuation, replan, or escalation is the next path

Review trace should not become a giant prose essay unless necessary.
A summary plus artifact references is preferred.

---

## Approval Trace

Approval trace records permission-gating events.

Typical approval trace moments include:

- approval requested
- approval running
- approval granted
- approval rejected
- approval escalated

### Approval trace should capture

- what required approval
- who or what authority handled it
- whether approval was granted or denied
- the concise reason for the outcome
- what the next allowed path is

Approval trace is about permission state, not review quality.

---

## Agent Trace

Agent trace records activity attributable to a named agent.

Typical agent trace moments include:

- executor assignment
- agent start of meaningful work
- major delegation
- major completion
- major failure
- repeated stall or non-progress signal

Agent trace should not attempt to serialize an agent's entire internal mental process.

Its purpose is accountability and operational visibility.

---

## Tool / Workflow Trace

Tool or workflow trace records the use of tools, external workflows, or pipeline-like execution surfaces.

Typical tool/workflow trace moments include:

- workflow invoked
- tool action completed
- pipeline failed
- external asset generated
- publish flow executed
- external job returned error

### Tool/workflow trace should preserve

- what tool or workflow was used
- why it was used
- whether it succeeded
- resulting artifact references
- bounded failure summary if relevant

Avoid copying raw large payloads into trace unless the payload itself is tiny and essential.

---

## Memory Trace

Memory trace records meaningful memory-affecting actions.

Typical memory trace moments include:

- durable memory added
- durable memory revised
- durable memory removed
- daily memory entry created
- lesson promoted from temporary note to durable memory

### Memory trace is important because

memory changes affect future behavior and future judgment.

Therefore, meaningful durable-memory changes should not be invisible.

Memory trace should capture:

- what changed
- why it changed
- what level of memory was affected
- whether the change was additive, revisive, or destructive

---

## Alert Trace

Alert trace records abnormal conditions or governance-significant warning events.

Typical alert trace moments include:

- stalled task detected
- repeated failure threshold reached
- high-risk action blocked
- escalation triggered
- approval conflict detected
- executor health problem surfaced

Alert trace should preserve:

- what triggered the alert
- severity
- affected object or task
- current response posture

---

## Minimum Trace Expectations

At minimum, meaningful trace should exist for:

- durable task creation
- major executor delegation
- major task state changes
- review outcomes
- approval outcomes
- significant failures
- replans
- escalations
- meaningful durable memory changes
- high-risk or blocked actions

If a task materially changes the system and leaves no traceable summary, governance visibility is too weak.

---

## High-Risk Trace Rule

High-risk work should produce stronger trace clarity.

As risk rises, trace should generally improve in:

- summary quality
- rationale clarity
- linkage quality
- review visibility
- approval visibility
- artifact reference quality

High-risk actions should not be the least traceable actions in the system.

### Permanent retention tendency

High-risk actions, vetoes, destructive attempts, major escalations, and structurally important governance events should tend toward durable retention.

This document does not define exact storage retention machinery,
but it does define the governance expectation that these traces matter more and should not be casually discarded.

---

## Long-Running Work Trace

Long-running work should preserve checkpoint-grade trace, not only final trace.

Typical long-running trace checkpoints include:

- epic created
- milestone started
- milestone completed
- milestone failed
- major replan
- long-run checkpoint summary
- executor handoff
- prolonged stall
- long-window completion or continuation decision

### Why

Without checkpoint trace, long-running work becomes hard to:

- supervise
- summarize
- recover
- review
- continue across sessions

---

## Checkpoint and Snapshot Terms

### checkpoint

A durable marker that captures meaningful progress and supports later continuation or review.

A checkpoint should usually preserve:

- summary
- current state
- major artifact references
- blocker status
- next decision posture

### snapshot

A compact reconstruction-friendly state capture.

Snapshots may be useful for long-running work,
but this document treats them as optional support mechanisms rather than mandatory universal trace fields.

---

## Trace and Memory Distinction

Trace and memory are related but not identical.

### Trace
Records what happened for audit, recovery, and accountability.

### Memory
Preserves what deserves to influence future judgment across sessions.

### Practical rule

Not every trace event should become memory.

Not every memory-worthy conclusion should be stored as raw trace.

Typical flow when lessons matter:

trace -> review/postmortem -> durable lesson -> memory summary

---

## Trace and Reporting Distinction

Trace supports reporting, but trace is not the same thing as report output.

Trace stores structured accountable signal.

Reports compress trace and current state into decision-friendly summaries.

A good report may draw from trace,
but should not require dumping trace wholesale into user-facing or operator-facing output.

---

## Trace and Raw Reasoning Restriction

This workspace does not treat raw internal chain-of-thought as normal trace material.

Instead, use:

- `summary`
- `reasoning_summary`
- `status_summary`

These fields preserve useful decision signal while avoiding uncontrolled reasoning storage.

This improves:

- compactness
- governance clarity
- privacy and safety posture
- future maintainability

---

## Artifact Reference Rule

Prefer `artifact_refs` over embedded bulk payloads.

Use references for:

- changed files
- commits
- generated media
- published outputs
- reports
- review documents
- specs
- workflow outputs

Inline large content only when:

- the content is very small
- the content is essential to understand the trace event
- using a reference would materially reduce clarity

Default posture:

reference first

---

## Trace Quality Rules

### Rule 1: summary first

Every meaningful trace should be understandable from its summary fields without requiring a massive narrative.

### Rule 2: preserve actor clarity

Where relevant, preserve who initiated, executed, and approved.

### Rule 3: preserve next control point

Trace should help the system understand what happens next:

- continue
- review
- approve
- replan
- escalate
- stop

### Rule 4: avoid duplication

If a packet, artifact, or step object already holds structure, trace should reference it rather than duplicate it heavily.

### Rule 5: trace should support failure recovery

A trace model that cannot help explain failure or resume long-running work is not sufficient.

---

## Relation to Other Documents

This document should align with:

- `STATE_MACHINE.md`
- `RISK_MODEL.md`
- `DEV_TASK_MODEL.md`
- `contracts/dev_task_packet.schema.json`
- `contracts/dev_result_packet.schema.json`
- `main-agent-step.schema.json`
- future `trace_event.schema.json`

This document defines trace semantics and expectations.

Future machine-readable schemas or trace validators should provide enforcement and structural guarantees.

---

## Failure Modes This Model Should Prevent

This trace model exists partly to prevent:

- invisible major decisions
- unaccountable executor behavior
- long-running work with no checkpoint visibility
- high-risk action with weak audit trail
- reports that cannot be traced back to actual events
- memory changes with no accountability
- trace stores filled with noise but lacking useful signal

---

## Final Principle

A good trace system does not record everything.

It records what must remain legible for accountability, recovery, and governance.

If trace becomes a swamp of duplicated noise, it stops protecting the system.

The correct trace model preserves signal, linkage, and consequence.