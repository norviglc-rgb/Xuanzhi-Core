# MEMORY_WRITE_POLICY.md

## Purpose

This document defines the write, rewrite, promotion, and deletion policy for memory in the 玄织 workspace.

Its purpose is to keep memory useful, low-noise, and structurally disciplined.

This policy exists to prevent:

- memory bloat
- noisy long-term recall
- accidental storage of process chatter
- confusion between durable memory and temporary context
- promotion of unverified observations into long-term guidance
- root-layer memory pollution

This document is normative for memory-writing behavior.

---

## Core Principle

Memory is not a transcript store.

Memory is a selective continuity system.

A memory item should be kept only if it improves future judgment, future routing, future collaboration quality, or future architectural coherence.

If a piece of information is unlikely to matter again, it should not be promoted into durable memory.

If a piece of information is useful only for the current moment, it should remain in a temporary layer.

---

## Memory Layers

### 1. `MEMORY.md`

Role:

Long-term summary and navigation layer.

Use for:

- stable preferences
- durable system-shape decisions
- major strategic focus
- durable lessons
- navigation pointers

Do not use for:

- daily execution logs
- long historical narratives
- verbose planning notes
- repeated progress updates
- full project summaries
- copied reference materials

### 2. `memory/YYYY-MM-DD.md`

Role:

Daily running context layer.

Use for:

- bounded short-term notes
- daily observations
- temporary context
- small reminders
- brief status notes
- candidate lessons not yet promoted

Do not use for:

- full transcripts
- large dumps of source content
- permanent policy
- durable architectural canon unless later promoted

### 3. Lower-layer governance or integration documents

Role:

Detailed durable knowledge that is too long or too specialized for long-term memory summary.

Use for:

- detailed governance rules
- operational playbooks
- integration procedures
- postmortems
- spec detail
- lessons that need full elaboration before abstraction

Long-term memory may point to these documents,
but should not absorb all of their content.

---

## Memory Write Test

Before writing any memory, 玄织 should check all of the following.

### Test 1: Durability

Is this likely to matter again beyond the current session or current day?

If no, do not write to durable memory.

### Test 2: Reusability

Will this information likely improve future judgment, routing, review, or cooperation?

If no, do not write to durable memory.

### Test 3: Signal Quality

Is this information concise enough and meaningful enough to improve recall without adding noise?

If no, either compress it or do not write it.

### Test 4: Layer Fit

Does this belong in:

- `MEMORY.md`
- `memory/YYYY-MM-DD.md`
- a lower-layer governance file
- a contract or policy artifact
- nowhere

If the correct layer is not `MEMORY.md`, do not force it into `MEMORY.md`.

### Test 5: Stability

Is this sufficiently stable, or is it still too provisional, emotional, local, or process-bound?

If it is still unstable, keep it temporary or do not write it.

---

## Write Destinations

### Write to `MEMORY.md` when the item is:

- stable
- high-value
- cross-session useful
- summary-level
- likely to shape future decisions repeatedly

Typical examples:

- the user prefers anti-drift critique
- the system uses Claude Code as default development executor
- root-layer files must remain thin
- detailed governance belongs in retrieval layers
- a repeatedly confirmed architectural lesson

### Write to `memory/YYYY-MM-DD.md` when the item is:

- recent
- provisional
- likely useful for a short period
- context-specific
- too raw to become durable memory yet

Typical examples:

- today's phase progress
- a temporary blocker
- a note about what was just revised
- a candidate lesson still being tested
- a short reminder tied to current work

### Write to lower-layer documents when the item is:

- long
- detailed
- procedural
- policy-heavy
- implementation-specific
- better represented as a formal spec or guideline

Typical examples:

- full memory write policy
- detailed postmortem
- governance rationale requiring sectioned explanation
- integration-specific retention rules

---

## What Should Be Written Conservatively

The following categories should be written with strong restraint:

- user preference claims based on one occurrence
- architectural conclusions from a single short discussion
- emotionally colored interpretation
- tentative lessons
- broad generalizations not yet validated
- highly detailed process observations
- raw brainstorming fragments

These may belong in daily notes first,
and only later be promoted if they remain valid.

---

## What Should Usually Not Be Written

The following should usually not be written into memory at all:

- raw chain-of-thought style content
- repetitive status chatter
- transient implementation noise
- copied large excerpts from source documents
- obvious facts recoverable elsewhere
- low-value micro-preferences
- temporary frustrations with no durable lesson
- verbose summaries of routine progress
- one-off stylistic choices that are unlikely to recur

Memory should not become a junk drawer.

---

## Promotion Rule

A note may be promoted from temporary memory into durable memory only when it shows evidence of persistence or repeated relevance.

Promotion is appropriate when at least one of the following is true:

- the same preference or lesson has appeared multiple times
- the decision changes future routing or architecture
- the lesson materially reduces future error
- the information affects system shape over multiple sessions
- the item has already survived beyond the immediate task context

Promotion should usually involve compression and abstraction.

Do not promote raw notes unchanged.

Preferred promotion pattern:

temporary note -> compressed insight -> durable memory entry

---

## Incident and Lesson Promotion

When failures or incidents occur, use the following progression where appropriate:

incident -> postmortem -> lessons_learned -> strategy_update

Not every incident deserves durable memory.

Promotion is appropriate only when the lesson is:

- generalizable
- reusable
- important enough to influence future governance or execution

A painful event alone is not enough.
It must become a reusable lesson.

---

## Rewrite Rule

When updating an existing memory item, prefer:

- replacing outdated phrasing
- compressing repeated entries
- merging duplicates
- sharpening the lesson
- removing expired context

Memory should become clearer over time, not just longer.

If a new entry substantially overlaps with an existing entry, prefer revision of the old entry rather than accumulation of a second nearly identical entry.

---

## Deletion Rule

A memory item should be removed or demoted when it becomes:

- obsolete
- contradicted by a stable newer decision
- too noisy to justify retention
- too local to one past task
- redundant with another sharper memory entry
- better represented in another layer

Deletion is not memory loss.
Deletion is memory hygiene.

---

## Compression Rule

When a memory item is useful but verbose, compress it before storing it.

Compression should preserve:

- the durable signal
- the future-use value
- the correct level of abstraction

Compression should remove:

- process detail
- temporary framing
- narrative padding
- repeated justification
- local context that will soon expire

Good memory entries are usually shorter than the discussion that produced them.

---

## Memory and Root-Layer Discipline

`MEMORY.md` is a root-layer file and must obey root-layer constraints.

Therefore:

- keep it high-signal
- keep it summary-level
- keep it compact
- keep it navigational
- move detail downward

If a memory-related idea requires long explanation, it belongs in a lower-layer file, not in `MEMORY.md`.

---

## Memory and Hardening

Some memory-related rules should remain prose-level.
Others should be hardened.

Hardening review is recommended when a memory rule affects:

- destructive deletion
- promotion thresholds tied to governance
- trace requirements for memory actions
- protected memory categories
- automation around write or rewrite behavior

Potential hardening destinations include:

- `memory_write_rules.yaml`
- validator logic
- trace event requirements

Do not assume all memory behavior should remain manual forever.

---

## Review Cadence

Memory should be reviewed periodically for hygiene.

Review goals:

- remove noise
- merge overlap
- sharpen durable lessons
- demote expired temporary material
- confirm that `MEMORY.md` remains summary-level
- confirm that daily notes are not silently becoming permanent archives

Memory review does not need to be constant,
but it should be regular enough to prevent quiet accumulation.

---

## Operational Rule for 玄织

When deciding whether to write memory, 玄织 should prefer caution over accumulation.

Default posture:

- write less
- compress more
- promote slowly
- revise instead of stacking
- downshift detail
- preserve only what improves future control

If uncertain, do not write to `MEMORY.md`.

If mildly useful but unstable, use daily notes.

If detailed and durable, store it in a lower-layer document and keep only a short pointer in long-term memory.

---

## Typical Healthy Outcomes

Healthy memory behavior looks like:

- `MEMORY.md` stays short and useful
- daily notes remain bounded
- durable lessons become clearer over time
- repeated noise is compressed rather than duplicated
- strategy-level continuity improves
- retrieval quality remains high

---

## Typical Failure Modes

Unhealthy memory behavior looks like:

- `MEMORY.md` becoming a running archive
- daily files becoming unbounded dumps
- one-off thoughts being promoted into durable truth
- repeated duplication instead of revision
- memory being used as a substitute for proper specs
- high-noise notes degrading future retrieval

---

## Final Principle

Memory should preserve what deserves to survive.

Everything else should either stay temporary, move downward, or disappear.