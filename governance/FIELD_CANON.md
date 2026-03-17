# FIELD_CANON.md

## Purpose

This document defines the canonical field naming and structural conventions for the 玄织 workspace.

Its role is to reduce:

- field drift
- alias sprawl
- schema inconsistency
- trace mismatch
- registry mismatch
- handoff packet ambiguity

This document is normative for machine-readable and semi-structured artifacts.

It applies especially to:

- `contracts/*.json`
- `policies/*.yaml`
- trace-like structures
- registry-like structures
- task and result packets
- future validation logic

If multiple names are used for the same concept, this document defines the preferred canonical choice.

---

## Canonical Naming Rules

### 1. Use snake_case

Canonical field names must use `snake_case`.

Preferred:

- `task_id`
- `risk_level`
- `owner_ref`
- `approval_state`

Avoid:

- `taskId`
- `riskLevel`
- `ownerRef`
- `approvalState`

### 2. Use singular names for singular values

Use singular names for single values.

Preferred:

- `task_id`
- `risk_level`
- `summary`
- `executor`

Use plural names only for list-like values.

Preferred:

- `artifact_refs`
- `risk_reasons`
- `allowed_transitions`
- `trigger_types`

### 3. Prefer explicit names over short ambiguous names

Prefer names that preserve meaning across files.

Preferred:

- `task_state`
- `step_state`
- `lifecycle_state`
- `review_state`
- `approval_state`
- `risk_level`
- `risk_score`

Avoid using overly generic top-level names such as:

- `state`
- `status`
- `type`
- `score`
- `data`
- `result`

unless the object is extremely local and unambiguous.

### 4. Use `_id` for identities and `_ref` for pointers

Use `_id` when the field identifies the current or canonical object.

Examples:

- `task_id`
- `step_id`
- `trace_id`
- `workflow_id`

Use `_ref` when the field points to another object, artifact, or external record.

Examples:

- `owner_ref`
- `repo_ref`
- `artifact_ref`
- `memory_ref`

### 5. Use `_at` for timestamps

Preferred time fields end in `_at`.

Examples:

- `created_at`
- `updated_at`
- `approved_at`
- `last_seen_at`
- `archived_at`

### 6. Use explicit numeric suffixes where helpful

Use suffixes that make stored values self-explanatory.

Preferred:

- `retry_count`
- `failure_count`
- `estimated_runtime_seconds`
- `heartbeat_interval_seconds`
- `cost_limit`
- `risk_score`

---

## Canonical Object Families

### Identity family

Use when an object must be distinctly identifiable.

Typical fields:

- `*_id`
- `name`
- `title`
- `description`

Examples:

- `task_id`
- `workflow_id`
- `agent_id`
- `trace_id`

### Ownership family

Use when responsibility or governance ownership matters.

Preferred fields:

- `owner_type`
- `owner_ref`

Use these instead of a single ambiguous `owner` field when structured ownership matters.

### Audit family

Use for origin and modification tracking.

Preferred fields:

- `created_at`
- `updated_at`
- `created_by`
- `updated_by`
- `approved_at`
- `approved_by`

### State family

Use distinct fields for distinct state domains.

Preferred fields:

- `task_state`
- `step_state`
- `review_state`
- `approval_state`
- `lifecycle_state`

Do not collapse these into a single `state` field when they have different semantics.

### Risk family

Preferred fields:

- `risk_level`
- `risk_score`
- `risk_summary`
- `risk_reasons`
- `risk_ceiling`

### Summary family

Preferred fields:

- `summary`
- `status_summary`
- `reasoning_summary`

Use these to preserve compressed signal rather than long prose.

### Routing and execution family

Preferred fields:

- `task_type`
- `executor`
- `recommended_executor`
- `execution_mode`
- `approval_mode`

### Linkage family

Preferred fields:

- `parent_task_id`
- `parent_step_id`
- `parent_trace_id`
- `artifact_refs`
- `repo_ref`

---

## Canonical Field Distinctions

### `task_id` vs `step_id`

- `task_id` identifies the main practical unit of work
- `step_id` identifies a bounded unit inside a task

Do not use one as the substitute for the other.

### `task_state` vs `step_state`

- `task_state` describes the task-level runtime condition
- `step_state` describes the step-level runtime condition

These must not be merged casually.

### `review_state` vs `approval_state`

- `review_state` describes evaluation status
- `approval_state` describes permission status

Review and approval are not the same process.

### `lifecycle_state` vs runtime state

- `lifecycle_state` describes durable administrative state
- runtime state fields such as `task_state` or `step_state` describe current execution condition

Do not reuse one for the other.

### `owner_type` / `owner_ref` vs `owner`

- `owner_type` + `owner_ref` are preferred in structured artifacts
- `owner` may still appear in prose, but should not be the preferred machine-facing form

### `risk_level` vs `risk_score`

- `risk_level` is categorical
- `risk_score` is more granular

Use both only when both meanings are actually needed.

### `summary` vs `reasoning_summary`

- `summary` = overall concise description of result or status
- `reasoning_summary` = concise explanation of why a path, decision, or proposal exists

### `artifact_refs` vs embedded payloads

- `artifact_refs` point to outputs or files
- large outputs should not be inlined into every packet unless necessary

Prefer references over payload sprawl.

---

## Task and Step Canon

### Task-level preferred fields

Use these fields for structured task-like objects when applicable:

- `task_id`
- `task_type`
- `summary`
- `task_state`
- `risk_level`
- `recommended_executor`
- `deliverable`
- `constraints`
- `created_at`
- `updated_at`

Optional but often useful:

- `approval_mode`
- `execution_mode`
- `repo_ref`
- `artifact_refs`
- `parent_task_id`

### Step-level preferred fields

Use these for bounded step-like objects when applicable:

- `step_id`
- `task_id`
- `summary`
- `step_state`
- `action`
- `expected_output`
- `risk_level`

Optional but often useful:

- `parent_step_id`
- `reasoning_summary`
- `artifact_refs`

If step structures become formalized, the schema should take precedence over prose examples.

---

## Handoff Packet Canon

### Task packet fields

For control-plane to executor handoff packets, preferred fields include:

- `task_id`
- `task_type`
- `summary`
- `goal`
- `deliverable`
- `constraints`
- `risk_level`
- `recommended_executor`
- `repo_ref`
- `approval_mode`
- `execution_mode`

### Result packet fields

For executor to control-plane result packets, preferred fields include:

- `task_id`
- `summary`
- `status_summary`
- `task_state`
- `artifact_refs`
- `risk_level`
- `review_state`

Optional but useful:

- `changed_files`
- `tests_run`
- `blockers`
- `next_step`
- `reasoning_summary`

If packet schemas later become formalized, those schemas become the enforcement layer, while this document remains the naming baseline.

---

## Registry Canon

### Agent registry preferred fields

Use when defining structured agent registry objects:

- `agent_id`
- `name`
- `description`
- `owner_type`
- `owner_ref`
- `risk_ceiling`
- `lifecycle_state`
- `created_at`
- `updated_at`

Optional but useful:

- `permissions`
- `capability_scope`
- `isolation_level`
- `heartbeat_interval_seconds`
- `last_seen_at`

### Workflow registry preferred fields

Use when defining structured workflow registry objects:

- `workflow_id`
- `name`
- `description`
- `owner_type`
- `owner_ref`
- `lifecycle_state`
- `risk_level`
- `created_at`
- `updated_at`

Optional but useful:

- `trigger_types`
- `permissions`
- `version`
- `approved_at`
- `approved_by`

---

## Trace Canon

For trace-like objects, prefer these fields:

- `trace_id`
- `task_id`
- `step_id`
- `summary`
- `reasoning_summary`
- `risk_level`
- `review_state`
- `approval_state`
- `created_at`
- `artifact_refs`

Optional but useful:

- `parent_trace_id`
- `executor`
- `status_summary`

Avoid turning trace structures into narrative dumps.

Trace should preserve useful audit signal, not full conversational sprawl.

---

## Memory Canon

For long-term memory summary entries or memory-related structured references, prefer:

- `summary`
- `category`
- `created_at`
- `updated_at`
- `artifact_refs`

For stable root-layer memory sections, prefer semantic grouping over pseudo-database over-structuring.

`MEMORY.md` should remain human-readable and summary-oriented.

Detailed memory rules belong in policy and governance files, not in root memory summary itself.

---

## Enumerated Field Guidance

This document does not try to freeze every enum value globally.

However, the following principle applies:

- enums should be explicit when stabilized
- enum meaning should be consistent across files
- enum changes should trigger schema and policy review where relevant

Likely enum-heavy fields include:

- `task_state`
- `step_state`
- `review_state`
- `approval_state`
- `lifecycle_state`
- `risk_level`
- `task_type`

When these become critical, they should be hardened in schemas or policy artifacts.

---

## Alias Avoidance Rule

Do not casually introduce parallel names for the same concept.

Examples of drift to avoid:

- `status` instead of `task_state`
- `kind` instead of `task_type`
- `owner` instead of `owner_type` + `owner_ref`
- `risk` instead of `risk_level`
- `output_refs` instead of `artifact_refs`
- `updated_on` instead of `updated_at`

If an alias already exists in legacy material, canonicalize toward the preferred field name in new work.

---

## Migration and Refactoring Rule

When a field is renamed or clarified:

1. identify the old name
2. identify the new canonical name
3. update schemas and policies where relevant
4. note the semantic reason for the change
5. avoid long-term dual usage

The goal is convergence, not permanent synonym coexistence.

---

## Practical Rule for New Files

When creating a new structured artifact:

1. prefer existing canonical field names
2. avoid inventing new top-level generic names
3. separate state domains explicitly
4. use `_id`, `_ref`, and `_at` consistently
5. keep summaries concise and reusable
6. prefer artifact references over embedded bulk output
7. trigger hardening review if the structure becomes important

---

## Final Principle

Field naming is not cosmetic.

When fields drift, structure drifts.
When structure drifts, validation, routing, memory, trace, and reporting all become harder.

This canon exists to keep structured artifacts convergent as the workspace grows.