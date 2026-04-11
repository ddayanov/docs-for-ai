---
standing: proposed
---

# Project Operating Agreement

This document is a proposed bill. It is not yet part of the governing stack. Projects may adopt it, trial it, amend it, or reject it. Adoption is recorded in the project's own continuity. Rejection requires no justification.

If a project adopts this bill, the decisions it defines must be made explicitly and recorded before consequential work begins. The bill does not supply the answers. It defines the questions that cannot be left unanswered.

---

## What This Bill Covers

Six categories of decisions that human-AI partnerships must make explicitly. In each category, the bill names the decision, names the default when no decision is recorded, and names where the answer must live.

---

## 1. Infrastructure Authority

Every project must decide: what actions may an AI model take on shared infrastructure without explicit per-action human approval?

Shared infrastructure includes version control commits, pushes, deployments, external service calls, and any action that is difficult or impossible to reverse. The spectrum runs from full human gate on every action to full delegation for a defined class of changes. Either end is valid. The middle requires precision.

The answer must be recorded in the project's entry file or working agreement. Silence is not delegation. When no decision is recorded, the default is: human approval required before any action on shared infrastructure.

---

## 2. Model Coordination

Every project with more than one AI model must decide: how are surfaces claimed, how are conflicts surfaced, and how are handoffs conducted?

This is not a role assignment. Roles change. The coordination protocol does not have to change with them. The project must record: how a model declares its intent to work on a surface, what another model does when it discovers a conflict with an in-progress claim, and how state is transferred when one model hands off to another.

When no protocol is recorded, the default is: read the active state surface before acting on any shared file, and surface conflicts to the human before proceeding.

---

## 3. Economics

Every project doing consequential or expensive operations must decide: what requires explicit human approval before it begins?

Expensive operations include compute-intensive runs, infrastructure changes with cost implications, destructive operations, and any action where the cost of being wrong is high relative to the cost of asking. The project must record its thresholds — not as a bureaucratic checklist, but as a clear line that any model can evaluate without ambiguity.

When no thresholds are recorded, the default is: name the cost before beginning any operation that cannot be interrupted or reversed cheaply.

---

## 4. Working Agreement

Every project doing multi-session consequential work should have a working agreement.

A working agreement is a short, structured record of how the human and AI will operate together for a specific type of work. It is not process theater. It is operational alignment made explicit so that decisions during the work are consistent with decisions before it.

At minimum, a working agreement should record: the primary goal for the current operation, the rollback and checkpoint policy, the main success criterion, and how failure types are distinguished. A working agreement may be as short as four lines. It may be invoked at the start of any serious session.

A working agreement is a living document. It improves through use. When the collaboration produces feedback, that feedback belongs in the working agreement or in a companion collaboration record — not lost at the session boundary.

---

## 5. Debate and Decision

Disagreement between models is expected and legitimate. Concealed disagreement is not.

Every project must decide: when models disagree on approach, how is the disagreement resolved and how is the decision recorded?

The bill establishes one constraint that is not negotiable: unresolved model disagreement must surface to the human as a named conflict before either model proceeds. Silent resolution — where one model simply acts and the other's position disappears — is not resolution. It is suppression.

When a decision emerges from debate, the record must carry the dissenting position alongside the chosen path. Future participants need to know what was considered and rejected, and why, not only what was chosen.

---

## 6. Feedback and Adaptation

The operating relationship between human and AI is not fixed at project start. It improves through direct feedback. That improvement is legitimate project continuity.

Every project should record what works, what slows work down, and what the partnership has learned. This record belongs in the project's continuity surfaces — not in conversation history that does not survive session boundaries.

Collaboration feedback is not administrative overhead. It is the mechanism by which the partnership becomes more capable over time. A project that discards this feedback at every boundary restarts the relationship from the same baseline indefinitely.

---

## Adoption

To adopt this bill, a project records in its own continuity: which sections it adopts, what decisions it has made for each, and the date of adoption.

Partial adoption is valid. A project may adopt sections 1 and 4 and defer the rest. A project may adopt the bill with amendments. What a project may not do is claim adoption while leaving decisions unanswered — the bill's purpose is to force the questions into the open, not to produce nominal compliance.

To reject or withdraw from this bill, the project records the withdrawal and states what, if anything, replaces the decisions the bill would have required.

---

## Standing

This bill is proposed. It is under trial in projects that choose to adopt it. Evidence from those trials — what works, what is too prescriptive, what is missing — should be returned to the governing stack through the normal observation and incident record process. The bill will be amended or adopted into the governing stack when the evidence supports it.
