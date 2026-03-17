# RULE_HARDENING_POLICY.md

## Purpose

This document defines the hardening policy for governance rules in the 玄织 system.

Its purpose is to prevent long-term drift into a prose-only governance architecture.

Narrative governance documents are necessary, but they are not sufficient for stable execution.

This policy exists to ensure that when rules become important enough, they are progressively translated into stronger machine-readable forms such as:

- JSON Schema
- YAML policy
- validator logic
- state transition tables

This document is normative for rule evolution.

If a new governance rule is added or an existing rule is changed, this policy defines the minimum hardening review that must occur before the change is considered complete.

---

## Core Principle

A rule written only in prose is a rule that still depends on interpretation.

Interpretation is useful for human understanding,
but insufficient for reliable control when the rule governs:

- structure
- permissions
- lifecycle
- state transitions
- risk decisions
- approvals
- registry integrity
- trace integrity
- memory safety

Therefore, the system must not indefinitely rely on prose-only governance for rules that materially affect execution, authority, or recoverability.

---

## Design Position

This policy does not require every rule to be immediately executable.

That would be excessive and impractical.

Instead, this policy requires that every meaningful new or modified rule be evaluated for hardening suitability.

The required question is not:

"Can we leave this in Markdown for now?"

The required question is:

"Should this rule remain prose-only, or does it now deserve a machine-readable counterpart?"

If uncertainty remains, the rule should be flagged for hardening review rather than ignored.

---

## Scope

This policy applies to all governance and operating rule changes, especially those affecting:

- `AGENTS.md`
- `SOUL.md`
- `USER.md`
- `MEMORY.md`
- `governance/*.md`
- `contracts/*.json`
- `policies/*.yaml`

It is especially important for changes involving:

- object fields
- required metadata
- state semantics
- risk classification
- approval behavior
- registry requirements
- workflow activation
- memory operations
- trace minimums
- durable task handoff contracts

---

## Why This Policy Exists

Without rule hardening discipline, the system tends to drift toward a fragile pattern:

1. a rule is written in prose
2. similar rules are later added elsewhere
3. enforcement remains implicit
4. runtime behavior diverges from documentation
5. conflicts accumulate
6. debugging becomes governance archaeology

This policy exists to prevent that pattern.

The goal is not bureaucratic heaviness.

The goal is to keep the system governable as it grows.

---

## Rule Classes

Every governance rule should be thought of as belonging to one or more rule classes.

### Class A: Semantic Rule

A rule that defines meaning, terminology, or conceptual distinction.

Examples:

- the difference between `task_state` and `step_state`
- the difference between `capability_scope` and `permissions`
- the meaning of `risk_ceiling`
- the meaning of `MEMORY.md`

Typical destination:

- `governance/GOVERNANCE_GLOSSARY.md`
- `governance/FIELD_CANON.md`
- narrative governance specifications

These rules may remain prose-first,
but they still require consistency review across files.

### Class B: Structural Rule

A rule that defines required fields, field names, field shapes, enums, or object constraints.

Examples:

- required fields for a step object
- required fields for agent registry entries
- allowed values for `workflow_type`
- required audit fields

Typical hardening destination:

- JSON Schema
- field canon
- validator logic

### Class C: Policy Rule

A rule that governs allow/deny behavior, thresholds, approval paths, permissions, or routing gates.

Examples:

- approval required before workflow activation
- R4 means immediate block
- no agent may exceed `risk_ceiling`
- destructive memory delete requires escalation

Typical hardening destination:

- YAML policy
- controller policy engine
- validator logic

### Class D: Transition Rule

A rule that governs lifecycle transitions or state movement.

Examples:

- `approved` before `active`
- retry before replan
- review failure -> replan
- approval rejection -> replan
- max retry behavior
- stalled inspection routing

Typical hardening destination:

- state transition table
- state validator
- scheduler/controller logic

### Class E: Operational Rule

A rule that governs process posture, writing practice, review flow, or maintenance discipline.

Examples:

- root files should stay thin
- daily review should include running tasks and running agents
- long-term memory writes must be conservative
- all meaningful structural changes should be documented

These rules may remain prose-first,
but should still be evaluated for partial hardening where useful.

---

## Mandatory Hardening Review

Every meaningful rule addition or modification must undergo a hardening review.

This review is mandatory.

The question is not whether hardening must happen immediately.
The question is whether hardening has been assessed.

The hardening review consists of four required checks.

---

## The Four Required Hardening Checks

### Check 1: Schema Check

Ask:

Does this rule define or change any of the following?

- required fields
- field names
- field types
- enums
- object structure
- packet format
- metadata requirements
- lifecycle field presence
- trace field presence

If yes, assess whether the rule should update or create:

- JSON Schema
- field canon entry
- validation logic

Typical targets:

- `main-agent-step.schema.json`
- `dev_task_packet.schema.json`
- `dev_result_packet.schema.json`
- `agent_registry.schema.json`
- `workflow_registry.schema.json`
- `trace_event.schema.json`

### Check 2: Policy Check

Ask:

Does this rule define or change any of the following?

- allow / deny behavior
- risk thresholds
- approval requirements
- escalation criteria
- write permissions
- trigger constraints
- routing logic
- governance veto conditions

If yes, assess whether the rule should update or create:

- YAML policy
- allowlist / denylist rule
- controller-side policy enforcement logic

Typical targets:

- `risk_policy.yaml`
- `approval_rules.yaml`
- `memory_write_rules.yaml`

### Check 3: Validator Check

Ask:

Does this rule require pre-execution, pre-registration, pre-activation, pre-write, or pre-merge validation?

If yes, assess whether validator logic is needed for:

- packet validation
- registry admission
- workflow activation
- memory write control
- review gating
- approval gating
- root file boundary enforcement

Validator need is especially strong when the cost of invalid state is high.

### Check 4: State Transition Check

Ask:

Does this rule affect:

- task state
- step state
- review state
- approval state
- lifecycle state
- retry behavior
- replanning behavior
- escalation behavior
- activation behavior
- pause/resume behavior

If yes, assess whether the rule should update or create:

- state transition table
- state guard logic
- scheduler/controller transition checks

Typical target:

- `state_transitions.yaml`

---

## Hardening Review Output

Every rule change must produce a hardening review summary.

This summary must include at least:

- rule change summary
- affected documents
- schema impact: yes/no + reason
- policy impact: yes/no + reason
- validator impact: yes/no + reason
- state transition impact: yes/no + reason
- proposed hardening targets
- immediate hardening required: yes/no
- deferred hardening allowed: yes/no + reason
- technical debt note if deferred

This output does not need to be large.

It does need to be explicit.

Silence is not an acceptable hardening decision.

---

## Immediate Hardening Triggers

Some rule changes should default to immediate hardening rather than optional later review.

Immediate hardening is strongly recommended when a rule affects:

- risk classification or risk enforcement
- approval boundaries
- workflow activation conditions
- registry required fields
- trace required fields
- memory delete or destructive memory operations
- lifecycle transitions
- state transitions
- protected or sensitive file operations
- executor handoff packet structure
- agent authority expansion
- permission changes
- sub-agent creation requirements

These are not ordinary narrative refinements.
They affect the governed behavior of the system.

---

## Deferred Hardening Rules

Not every rule must be hardened immediately.

Deferred hardening may be acceptable when all of the following are true:

- the rule is low-risk
- the rule is low-frequency
- the rule is mainly explanatory
- the rule has low enforcement cost if interpreted manually
- the rule does not create critical ambiguity
- the technical debt is documented

Examples of rules that may remain prose-first for a while:

- stylistic communication preferences
- explanation ordering preferences
- descriptive examples
- low-stakes narrative guidance
- non-critical maintenance heuristics

Deferral is acceptable.
Silent neglect is not.

---

## Hardening Priority Order

When hardening capacity is limited, use this priority order.

### Priority 1: Execution-critical contracts

Examples:

- task handoff packets
- result packets
- step object schema

### Priority 2: Risk and approval gates

Examples:

- risk policy
- approval rules
- destructive operation thresholds

### Priority 3: State and lifecycle controls

Examples:

- state transitions
- activation rules
- retry rules
- review failure behavior

### Priority 4: Registry integrity

Examples:

- agent registry schema
- workflow registry schema
- required audit fields

### Priority 5: Trace integrity

Examples:

- trace minimum fields
- retention-critical events
- artifact reference rules

### Priority 6: Memory write control

Examples:

- write / rewrite / delete gating
- promotion rules
- summary vs detail write boundaries

---

## Rule Change Categories and Expected Hardening

This section defines common cases and the expected hardening posture.

### Category: terminology clarification

Expected hardening:

- glossary or field canon update
- schema impact usually no
- policy impact usually no
- validator impact usually no
- state impact usually no

### Category: field rename or field standardization

Expected hardening:

- field canon update required
- schema review required
- validator review likely required
- transition impact depends on field function

### Category: risk rule change

Expected hardening:

- policy review required
- validator review likely required
- state impact possible
- immediate hardening often recommended

### Category: approval path change

Expected hardening:

- policy review required
- state transition review required
- validator review likely required

### Category: lifecycle change

Expected hardening:

- schema review likely required
- state transition review required
- validator review likely required

### Category: packet or trace shape change

Expected hardening:

- schema review required
- validator review required
- policy review optional
- state impact depends on semantics

### Category: memory write behavior change

Expected hardening:

- policy review required
- validator review often required
- trace review often required

### Category: root file boundary rule

Expected hardening:

- usually prose-first
- validator review may still apply for linting or guardrail tooling
- schema impact usually low

---

## Rule Hardening Debt

If a rule is judged to need hardening but is not hardened immediately, the system must create a hardening debt record.

The record should include:

- rule summary
- affected file
- affected layer
- why hardening is needed
- why hardening is deferred
- proposed target artifact
- severity
- review date or next review phase

This debt may live in:

- governance debt notes
- technical debt review
- weekly review
- a dedicated hardening backlog

The debt must remain visible.

Invisible hardening debt becomes system drift.

---

## Relation to Existing Governance Documents

This policy does not replace governance prose.

It complements it.

Typical relationship:

- prose explains the meaning
- contracts define the structure
- policies define the gate
- validators enforce the check
- state tables define legal movement

All five may coexist.

Good governance is layered, not mono-format.

---

## Relation to Root File Policy

`ROOT_FILE_POLICY.md` controls what should stay in thin root files.

This document controls what should be hardened when rules evolve.

The two policies should be applied together:

- root policy keeps constant prompt surface small
- hardening policy prevents deep rules from remaining forever soft

Together they reduce both context bloat and control softness.

---

## Operational Rule for the Main Agent

When the main agent proposes, edits, or reviews a governance rule, it must not stop at the prose layer by default.

It must also ask:

- does this change affect structure?
- does this change affect policy?
- does this change affect validation?
- does this change affect state movement?

If yes, it should either:

- update the corresponding machine-readable artifact
or
- create an explicit hardening debt note

Doing neither is non-compliant behavior.

---

## Operational Rule for Governance Review

Any governance review that accepts a non-trivial rule change should verify that a hardening review was actually performed.

The review should reject vague claims such as:

- "we can harden this later"
- "this is obvious enough"
- "the controller will probably handle it"
- "the model will remember"

These are not hardening decisions.
They are evasions.

---

## Typical Failure Patterns This Policy Prevents

### Failure Pattern 1: prose-only accumulation

Large governance documents grow, but runtime enforcement remains weak.

### Failure Pattern 2: duplicated rules with partial mismatch

A rule appears in multiple documents but is hardened nowhere.

### Failure Pattern 3: packet drift

The main agent and execution agent gradually disagree on structured handoff shape.

### Failure Pattern 4: state drift

Narrative descriptions of state behavior diverge from scheduler/controller behavior.

### Failure Pattern 5: registry softness

Registry fields are described in prose but not actually validated.

### Failure Pattern 6: delayed hardening forever

The system repeatedly says it will harden "later" until drift becomes expensive.

---

## Compliance Signals

Healthy signals:

- rule changes trigger hardening checks automatically
- important rules have clear machine-readable counterparts
- prose and contracts remain aligned
- state and risk rules become more explicit over time
- packet schemas stabilize
- governance discussions create fewer contradictions

Unhealthy signals:

- repeated prose changes with no hardening review
- conflicting behavior between documents and execution
- missing schema updates after field changes
- repeated "to be hardened later" with no backlog tracking
- unclear state or approval behavior at runtime

---

## Exception Rule

An exception to hardening review is allowed only for changes that are clearly:

- editorial
- formatting-only
- non-semantic
- non-structural
- non-operational

Examples:

- typo fixes
- grammar changes
- wording clarity improvements that do not alter meaning

If meaning changes, this policy applies.

---

## Final Principle

A mature governance system does not merely describe itself.

It increasingly makes its critical rules legible to machines as well as humans.

Prose gives meaning.
Hardening gives control.

Both are necessary.