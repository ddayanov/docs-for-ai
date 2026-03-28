# Ever-Evolving Context Schema

The operating document defines the standard.
This document gives that standard a shape that tools, repos, and workflows can actually hold.

A schema that nobody maintains is not a schema.
It is aspiration formatted as metadata.

This one is intentionally narrow.
It should be strong enough to prevent drift and light enough to survive real use.

---

## Core Objects

The system is built from seven object types:

1. `context_item`
2. `decision`
3. `continuity_event`
4. `update_event`
5. `handoff_packet`
6. `contradiction`
7. `session_record`

These can live in markdown, JSON, YAML, a database, or a terminal tool.

The storage format is secondary.
The structure is what matters.

The schema exists to support active continuity. A context system that only stores information but cannot signal that the picture needs repair is not maintaining continuity strongly enough.

The schema must also reflect the asymmetry of continuity work. Some truth is already present in the project and can be maintained, compared, invalidated, and transferred by the AI directly. Some truth still exists only with the human and must be brought into the project before continuity can be restored. A continuity system that cannot distinguish between those two conditions will either wait too passively or ask the human to do work the system should already be doing itself.

---

## 1. context_item

This is the atomic unit of project context.

It can represent a fact, a constraint, a claim, a summary, a bottleneck, an assumption, or any other piece of project truth that the system must carry forward.

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
  The actual claim or summary.
- `source_type`
  One of: `human`, `repo`, `runtime`, `measurement`, `document`, `model`
- `source_ref`
  Pointer to the evidence or origin.
- `updated_at`
  Time of the current version.
- `owner`
  Human or model responsible for the current version of the item.

### Useful Optional Fields

- `revision_anchor`
  Commit, branch, environment, deploy id, or other freshness anchor.
- `confidence`
  Useful when status is `inferred`.
- `expires_on_change`
  Conditions that make the item stale.
- `related_ids`
  Links to decisions, contradictions, or neighboring context items.
- `tags`
  Example: `objective`, `constraint`, `bottleneck`, `architecture`, `verification`
- `update_needed`
  Boolean indicating that the item is known to require refresh or confirmation before safe use.
- `update_request`
  A short statement of what needs to be updated and by whom if the owner cannot complete it alone.
- `knowledge_scope`
  One of: `project_visible`, `human_only`, `mixed`
- `maintenance_mode`
  One of: `ai_primary`, `human_primary`, `shared`
- `human_input_required`
  Boolean indicating that continuity cannot be restored for this item from project-visible evidence alone.

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
owner: "codex"
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

- `alternatives_considered`
- `supersedes`
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

This object records a material change while continuity repair is still in progress.

It is the mechanism by which context becomes ever-evolving rather than merely updated after the fact. A continuity event carries the trigger for change, the reason it matters, what lost authority, what surfaces now require repair, and what must happen before the project can be treated as settled again.

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
- `human_input_required`
- `preferred_resolver`
  One of: `ai`, `human`, `shared`
- `next_expected_action`
- `related_context_ids`
- `related_decision_ids`

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
  - "The assumption that update_event alone is sufficient."
required_repairs:
  - "Add continuity_event to the governing text."
  - "Add continuity_event object to the schema."
status: "repairing"
preferred_resolver: "ai"
next_expected_action: "Patch both continuity documents in the same continuity event."
```

---

## 4. update_event

This object records a change that may invalidate part of the current picture.

If context drift is the disease, update events are the moments where the system is forced to notice reality moved.

### Required Fields

- `id`
- `event_type`
  One of: `objective_change`, `constraint_change`, `repo_change`, `decision_made`, `verification_result`, `incident`, `handoff`, `environment_change`
- `summary`
- `occurred_at`
- `detected_by`
- `affected_context_ids`

### Useful Optional Fields

- `stales_ids`
  Context items made stale by the event.
- `creates_ids`
  Context items created because of the event.
- `followup_required`
- `followup_action`
- `context_update_required`
  Boolean indicating that stable or live context must be updated before continuation.
- `preferred_resolver`
  One of: `ai`, `human`, `shared`
- `human_input_required`
  Boolean indicating that the missing truth cannot be recovered from the project alone.

### Example

```yaml
id: upd_verify_014
event_type: verification_result
summary: "Benchmark disproved previous assumption about disk pressure."
occurred_at: "2026-03-27T22:15:00Z"
detected_by: "claude"
affected_context_ids:
  - "ctx_bottleneck_001"
stales_ids:
  - "ctx_assumption_003"
followup_required: true
followup_action: "Update working bottleneck and regenerate handoff packet."
```

---

## 5. handoff_packet

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
- `relevant_context_ids`
- `open_questions`
- `blockers`
- `next_expected_action`
- `prepared_at`
- `prepared_by`

### Useful Optional Fields

- `recent_changes`
- `verified_artifacts`
- `files_in_play`
- `warnings`
- `do_not_reopen`
  Paths already resolved and not worth revisiting without new evidence.
- `context_repairs_required`
  Updates the receiver must make, or request, before the handoff is safe to act on.
- `ai_repairs_pending`
  Repairs the receiving AI should complete directly from project-visible evidence.
- `human_inputs_pending`
  Missing truths the receiving AI must request from the human before safe continuation.

### Example

```yaml
id: handoff_021
objective: "Reduce training wall-clock time without increasing infra footprint."
current_task: "Redesign merge stage for parallel reduction."
current_state: "Profiling complete; serialized reducer confirmed as current bottleneck."
revision_anchor: "git:8f3c1ae"
relevant_context_ids:
  - "ctx_bottleneck_001"
  - "dec_storage_002"
open_questions:
  - "Can reduction shard by partition without violating output ordering?"
blockers:
  - "Need confirmation on ordering guarantees."
next_expected_action: "Design parallel merge alternatives and verify ordering constraints."
prepared_at: "2026-03-27T22:20:00Z"
prepared_by: "human"
verified_artifacts:
  - "benchmarks/merge-run-2026-03-27.md"
do_not_reopen:
  - "Do not revisit disk-backed intermediate storage unless memory evidence changes."
```

---

## 6. contradiction

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
- `created_update_event_id`

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
created_update_event_id: "upd_verify_014"
```

---

## 7. session_record

This object records the boundary itself.

It does not exist for archival comfort.
It exists so that the session start and session end are connected by something more reliable than memory.

### Required Fields

- `id`
- `project`
- `started_at`
- `ended_at`
- `participants`
- `start_packet_ref`
- `end_packet_ref`

### Useful Optional Fields

- `major_changes`
- `decisions_made`
- `verification_done`
- `context_gaps_found`
- `context_updates_requested`
  Updates or repairs that were surfaced but not completed inside the session.
- `ai_updates_completed`
  Continuity repairs completed directly by the AI during the session.
- `human_inputs_requested`
  Missing realities the AI had to request because they were not project-visible.

### Example

```yaml
id: session_044
project: "apn-platform"
started_at: "2026-03-27T20:00:00Z"
ended_at: "2026-03-27T22:30:00Z"
participants: ["human", "codex", "claude"]
start_packet_ref: "handoff_020"
end_packet_ref: "handoff_021"
major_changes:
  - "Confirmed serialized reducer as bottleneck."
verification_done:
  - "merge-run-2026-03-27.md"
context_gaps_found:
  - "Output ordering guarantee still not explicit."
```

---

## Required Operations

Any implementation that claims to maintain ever-evolving context must support these operations:

1. `create_context_item`
2. `update_context_item`
3. `mark_stale`
4. `supersede_item`
5. `record_decision`
6. `open_continuity_event`
7. `close_continuity_event`
8. `record_update_event`
9. `open_contradiction`
10. `resolve_contradiction`
11. `generate_handoff_packet`
12. `close_session`
13. `restore_session`
14. `request_context_update`
15. `apply_project_visible_update`
16. `request_human_truth`

If the system cannot do these, it is not maintaining context.
It is storing notes and hoping a human will perform the missing logic manually.

---

## Freshness Logic

Freshness is not a feeling.
It is computed against change.

A `context_item` should be considered stale when:

- its `revision_anchor` no longer matches project reality
- an `update_event` names it as stale
- a `contradiction` remains open against it
- one of its `expires_on_change` conditions has been triggered

Derived items inherit staleness from the canonical or working items they summarize.

If a summary is built on stale items, the summary is stale.

If an item is marked `project_visible` and `ai_primary`, the default expectation is direct AI upkeep. If it is marked `human_only` and `human_input_required`, the default expectation is explicit request rather than silent guesswork.

An open `continuity_event` is also a freshness signal. Any surface listed in its `affected_surfaces` should be treated as potentially transitional until the event is closed.

---

## Contradiction Resolution

When contradiction appears:

1. do not silently overwrite the older context
2. open a `contradiction`
3. identify the higher-authority source
4. mark affected items `stale` or `superseded`
5. create an `update_event`
6. regenerate the derived artifacts built on the invalidated picture

If the participant detecting the contradiction cannot repair the continuity surfaces directly, the system must still carry an explicit request for that repair. Continuity cannot depend on the hope that the next participant will notice the same gap independently.

Contradiction is not noise in the data.
It is how the system preserves honesty under change.

---

## Continuity Event Resolution

When a material change begins:

1. open a `continuity_event`
2. record the trigger and the reason
3. name what lost authority
4. list the surfaces that require repair
5. record whether human input is required
6. keep the event open until the affected surfaces are aligned

If the event is not opened, the project is forced to infer the change after the fact. That weakens continuity exactly where continuity should be strongest.

---

## Minimal Repo Mapping

For teams or projects that want to run the system manually before tooling exists, the schema can map to a repo with a small number of stable surfaces:

- `project.md`
  Canonical objective and constraints, typically human-originating
- `state.md`
  Current working context, typically AI-maintained
- `decisions.md`
  Decision objects
- `handoffs/`
  Handoff packets by session or milestone, including pending repairs and missing human input
- `verification/`
  Evidence artifacts referenced by context items
- `sessions.md`
  Session records, update events, and unresolved continuity requests

That is enough to begin.

The system can become more sophisticated later.
The discipline cannot be deferred until later.

---

## The Test

A context system based on this schema is working if:

- a new human or model can continue without narrative reconstruction
- stale claims are detectable instead of socially felt
- contradictions become explicit objects instead of vague discomfort
- current truth is easier to find than old discussion
- session start cost keeps dropping over time

If those things are not happening, the system is not holding context strongly enough yet.
