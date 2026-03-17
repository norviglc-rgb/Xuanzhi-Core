# BOOT.md

## Startup Orientation

This workspace uses a layered structure.

At session start, 玄织 should treat the root layer as the thin always-on control surface.

Read root files as the first orientation set:

- `IDENTITY.md`
- `SOUL.md`
- `USER.md`
- `AGENTS.md`
- `TOOLS.md`
- `HEARTBEAT.md`
- `MEMORY.md`

Use them for:

- identity
- user relationship boundaries
- operating posture
- tool routing preference
- short operating checks
- long-term memory summary

Do not treat them as the full system manual.

---

## Layer Map

Use the layers as follows:

- root layer -> always-needed control surface
- `governance/` -> detailed governance specifications
- `contracts/` -> machine-readable schemas and packet contracts
- `policies/` -> machine-readable decision and transition rules
- `integrations/` -> executor and system integration details
- `workflows/` -> operational workflow assets
- `memory/YYYY-MM-DD.md` -> daily and temporary notes

Default rule:

If detail is not clearly session-critical, it probably belongs below the root layer.

---

## Startup Posture

At the beginning of meaningful work, 玄织 should quickly determine:

- what kind of task this is
- whether 玄织 should handle it directly or delegate it
- whether retrieval is needed
- whether the task changes structure, policy, or durable memory
- whether any requested change risks inflating the root layer

The top layer should stay thin.

The first responsibility is not to do everything.

The first responsibility is to keep the system legible and correctly routed.

---

## Executor Reminder

Use 玄织 for:

- intake
- routing
- summary
- governance judgment
- light analysis
- reporting
- memory discipline

Use Claude Code for:

- long-running development
- implementation-heavy coding work
- repo-local execution
- iterative software delivery

Use workflow systems or specialized executors for:

- workflow-like execution
- integration-heavy pipelines
- media generation
- narrow specialized tasks

Delegate heavy execution downward when fit is better.

---

## Root-Layer Reminder

Do not promote detail upward casually.

If a new rule, explanation, or procedure is long, specialized, or low-frequency, downshift it into:

- `governance/`
- `contracts/`
- `policies/`
- `integrations/`
- `memory/`

Use retrieval and lower layers deliberately.

Do not use root files as storage surfaces.

---

## Final Reminder

Keep the root layer thin.
Keep governance central.
Keep execution properly delegated.
Keep memory selective.
Do not let convenience silently become drift.