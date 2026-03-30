# Ever-Evolving Context Schema

The operating document defines the standard.
This document gives that standard a shape that tools, repos, and workflows can actually hold.

A schema that nobody maintains is not a schema.
It is aspiration formatted as metadata.

This one is intentionally narrow.
It should be strong enough to prevent drift and light enough to survive real use.

---

## Core Objects

The system is built from five object types:

1. `context_item`
2. `decision`
3. `continuity_event`
4. `handoff_packet`
5. `contradiction`

These can live in markdown, JSON, YAML, a database, or a terminal tool.

The storage format is secondary.
The structure is what matters.

The schema exists to support active continuity. A context system that only stores information but cannot preserve truth across change and boundary is not maintaining continuity strongly enough.

---

## 1. context_item

This is the atomic unit of project truth.

It can represent a fact, a constraint, a claim, a summary, a bottleneck, an assumption, or any other piece of context the project must carry forward.

### Required Fields

- `id`
  Stable identifier.
- `title`
  Short label humans and models can refer to quickly.
- `layer`
  One of: `canonical`, `working`, `derived`
- `status`
  One of: `canonical`, `observed`, `verified`, `inferred`, `assumed`, `stale`, `superseded`
- `content`
  The claim itself.
- `source_type`
  One of: `human`, `repo`, `runtime`, `measurement`, `document`, `model`
- `source_ref`
  Pointer to the evidence or origin.
- `updated_at`
  Time of the current version.

### Useful Optional Fields

- `revision_anchor`
  Commit, branch, deploy id, benchmark id, or other freshness anchor.
- `tags`
  Example: `objective`, `constraint`, `bottleneck`, `verification`
- `related_ids`
  Links to decisions, contradictions, or neighboring context items.
- `expires_on_change`
  Conditions that make the item stale.

### Example

```yaml
id: ctx_bottleneck_001
title: Current Bottleneck
layer: working
status: observed
content: "Embedding merge stage is single-threaded and dominates wall-clock time."
source_type: measurement
source_ref: "benchmarks/merge-run-2026-03-27.md"
revision_anchor: "git:8f3c1ae"
updated_at: "2026-03-27T21:10:00Z"
tags: ["bottleneck", "performance"]
```

---

## 2. decision

This object records a choice that still governs the work.

A decision is not just what was chosen.
It is why it was chosen and what evidence would justify reversing it.

### Required Fields

- `id`
- `title`
- `decision`
- `reason`
- `made_at`
- `made_by`
- `inputs`
  References to the context items, measurements, or constraints that justified the choice.
- `reversal_condition`
  The evidence threshold that would reopen the decision.

### Useful Optional Fields

- `superseded_by`
- `impact_scope`
  Example: `architecture`, `infra`, `schema`, `workflow`

### Example

```yaml
id: dec_storage_002
title: Keep Runtime Working Set In Memory
decision: "Use RAM as the primary working surface; disk remains an artifact boundary."
reason: "Disk-bound architecture wasted the instance and inflated wall-clock time."
made_at: "2026-03-27T22:00:00Z"
made_by: "human"
inputs:
  - "ctx_bottleneck_001"
reversal_condition: "Revisit if working set exceeds stable memory bounds or memory pressure degrades throughput."
impact_scope: "architecture"
```

---

## 3. continuity_event

This object records material change while continuity repair is still in progress.

It is the mechanism by which context becomes ever-evolving rather than merely updated after the fact. A continuity event carries the trigger for change, the reason it matters, what lost authority, what surfaces require repair, and what must happen before the project can be treated as settled again.

Its timing matters as much as its contents. When local continuity surfaces exist, the continuity event is opened or updated before the material change is applied. If the change lands first, the project is reconstructing continuity after the fact.

The event must be visible, but it does not need its own file by default. A continuity event may be carried inside the project's existing live-state surface or equivalent local continuity area. Separate event files are a scaling choice, not a starting requirement.

Routine upkeep is not a continuity event. If truth already moved and the surface is only catching up, update the surface directly and quietly. A continuity event exists for material change: the moments when the working picture is about to move and the transition must be made visible before another participant inherits the wrong state.

### Required Fields

- `id`
- `trigger_type`
  One of: `human_decision`, `constraint_change`, `repo_change`, `verification_failure`, `contradiction`, `production_signal`, `conceptual_shift`, `governing_stack_change`
- `trigger_source`
- `reason`
- `opened_at`
- `opened_by`
- `affected_surfaces`
- `invalidates`
- `required_repairs`
- `status`
  One of: `open`, `repairing`, `closed`

### Useful Optional Fields

- `revision_anchor`
- `next_expected_action`
- `human_input_required`
- `related_context_ids`

### Example

```yaml
id: ce_012
trigger_type: conceptual_shift
trigger_source: "codex session 2026-03-27"
reason: "Continuity requires a first-class event object; update-after-the-fact is too weak."
opened_at: "2026-03-27T23:10:00Z"
opened_by: "human"
affected_surfaces:
  - "ever-evolving-context.md"
  - "ever-evolving-context-schema.md"
invalidates:
  - "The assumption that update-after-the-fact is sufficient."
required_repairs:
  - "Add continuity_event to the governing text."
  - "Add continuity_event object to the schema."
status: "repairing"
next_expected_action: "Patch both continuity documents in the same continuity event."
```

---

## 4. handoff_packet

This is the transferable unit at a boundary.

It is the most important object in the system because session-boundary integrity depends on it.

A handoff packet is not a conversation summary.
It is a compact statement of current truth, current uncertainty, and the next required move.

### Required Fields

- `id`
- `objective`
- `current_task`
- `current_state`
- `revision_anchor`
- `open_questions`
- `blockers`
- `next_expected_action`
- `prepared_at`
- `prepared_by`

### Useful Optional Fields

- `relevant_context_ids`
- `recent_changes`
- `files_in_play`
- `warnings`
- `do_not_reopen`
  Paths already resolved and not worth revisiting without new evidence.

### Example

```yaml
id: handoff_021
objective: "Reduce training wall-clock time without increasing infra footprint."
current_task: "Redesign merge stage for parallel reduction."
current_state: "Profiling complete; serialized reducer confirmed as current bottleneck."
revision_anchor: "git:8f3c1ae"
open_questions:
  - "Can reduction shard by partition without violating output ordering?"
blockers:
  - "Need confirmation on ordering guarantees."
next_expected_action: "Design parallel merge alternatives and verify ordering constraints."
prepared_at: "2026-03-27T22:20:00Z"
prepared_by: "human"
relevant_context_ids:
  - "ctx_bottleneck_001"
  - "dec_storage_002"
do_not_reopen:
  - "Do not revisit disk-backed intermediate storage unless memory evidence changes."
```

---

## 5. contradiction

This object exists because contradiction must not remain implicit.

When the story and the evidence diverge, the divergence itself has to be carried by the system. Otherwise the drift remains social and informal, and the next participant inherits it blindly.

### Required Fields

- `id`
- `claim_id`
  The context item or decision being challenged.
- `contradicting_source`
- `description`
- `detected_at`
- `detected_by`
- `severity`
  One of: `low`, `medium`, `high`, `critical`
- `resolution_state`
  One of: `open`, `investigating`, `resolved`, `superseded`

### Useful Optional Fields

- `resolution`
- `resolved_at`
- `resolved_by`

### Example

```yaml
id: contra_007
claim_id: "ctx_assumption_003"
contradicting_source: "production metrics 2026-03-27"
description: "Memory pressure is not the current bottleneck; serialized CPU work is."
detected_at: "2026-03-27T22:12:00Z"
detected_by: "human"
severity: "high"
resolution_state: "resolved"
resolution: "Marked assumption stale and replaced with measured bottleneck context."
resolved_at: "2026-03-27T22:16:00Z"
resolved_by: "codex"
```

---

## Required Operations

Any implementation that claims to maintain ever-evolving context must support these operations:

1. `create_context_item`
2. `update_context_item`
3. `supersede_item`
4. `record_decision`
5. `open_continuity_event`
6. `close_continuity_event`
7. `flag_contradiction`
8. `resolve_contradiction`
9. `generate_handoff_packet`
10. `restore_session`

If the system cannot do these, it is not maintaining continuity.
It is storing notes and hoping a human will perform the missing logic manually.

For material change, the order is part of the contract:

1. `open_continuity_event`
2. `record_trigger_and_affected_surfaces`
3. `apply_material_change`
4. `repair_affected_surfaces`
5. `close_continuity_event`

If step three occurs before step one, continuity has already failed.

---

## Freshness Logic

Freshness is not a feeling.
It is computed against change.

A `context_item` should be considered stale when:

- its `revision_anchor` no longer matches project reality
- a `contradiction` remains open against it
- one of its `expires_on_change` conditions has been triggered
- an open `continuity_event` has already invalidated the picture it belongs to

Derived items inherit staleness from the canonical or working items they summarize.

If a summary is built on stale items, the summary is stale.

An open `continuity_event` is also a freshness signal. Any surface listed in its `affected_surfaces` should be treated as potentially transitional until the event is closed.

---

## Contradiction Resolution

When contradiction appears:

1. do not silently overwrite the older context
2. flag a `contradiction`
3. identify the higher-authority source
4. mark affected items `stale` or `superseded`
5. repair the affected derived artifacts

If resolving the contradiction changes more than one surface or materially changes the working picture, open or update a `continuity_event` before the repair proceeds.

Contradiction is not noise in the data.
It is how the system preserves honesty under change.

---

## Minimal Repo Mapping

The minimal repo mapping is the practical starting pattern for a project adopting this schema. It is not a rigid requirement.

A project may begin with fewer surfaces, even a single file carrying the objective, the current state, and the governing decisions, and grow additional surfaces when the cost of not having them exceeds the cost of maintaining them.

What is mandatory is not the number of files. What is mandatory is that the project carries, in some durable form:

- the objective
- the current state
- the decisions that still govern the path
- a way to signal material change before it lands
- a way to transfer the picture across a boundary

If those are present, continuity is possible regardless of how many files hold them.
If any one of them is absent, continuity depends on memory and conversation, which do not survive boundaries.

One practical starting pattern looks like this:

- `project.md`
  Canonical objective and constraints
- `state.md`
  Current working context, including the active continuity event when dedicated event files are not yet warranted
- `decisions.md`
  Governing decisions when they have earned a separate surface
- `handoffs/`
  Boundary packets when handoffs are frequent enough to need dedicated space
- `verification/`
  Evidence artifacts referenced by context items

The project grows into this structure when the cost of not having it exceeds the cost of maintaining it.

---

## The Test

A context system based on this schema is working if:

- a new human or model can continue without narrative reconstruction
- stale claims are detectable instead of socially felt
- contradictions become explicit instead of vague discomfort
- material change becomes visible before it lands
- completion of the current task is reflected in live state before a new next action is named
- current truth is easier to find than old discussion
- handoffs carry enough truth that the next participant can continue correctly

If those things are not happening, the system is not holding context strongly enough yet.
