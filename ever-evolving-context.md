# Ever-Evolving Context

This document defines the continuity standard for human-AI work.

`the-conditions-of-engineering.md` establishes the physical and intellectual ground the work stands on. `operating-standards.md` defines how the work is scored, reasoned about, verified, and delivered. This document defines how the work remains continuous across sessions, participants, and change.

Human-AI work produces large amounts of plausible output. Continuity prevents that output from detaching from the project it is meant to serve.

Continuity requires vigilance. Human and AI do not preserve it by intensity of feeling, and not by politeness alone. They preserve it by noticing when the picture has moved, when the artifacts that carry it have not, and by repairing that gap before the work continues. Respect remains necessary. Vigilance is what gives respect operational force.

---

## Continuity

Continuity is the survival of the current working picture of the project across change.

That picture contains the objective, the current state of the work, the constraints actually in force, the decisions that still govern the path, the evidence that matters, the uncertainty that remains unresolved, and the next move the work requires.

When that picture survives a boundary intact, the work compounds.
When it does not, the work restarts under the appearance of progress.

Ever-evolving context means the working picture evolves with the project, so continuity remains real.

---

## Boundaries

Continuity is tested at boundaries.

A session boundary is one example. A model handoff is another. A human handoff is another. A large code change, a branch change, a benchmark that overturns the current theory, production behavior that contradicts the design, a subtle pivot in the objective, or a newly discovered constraint all create the same obligation.

The project must cross the boundary with an updated working picture.

If the picture crossing the boundary is stale, continuity is broken.

Most expensive failures in human-AI work begin there. The conversation still sounds coherent. The repository still looks familiar. The participants still believe they are continuing the same work. The picture is already old.

---

## The Standard

The working picture of the project must remain in honest alignment with the project as it actually is.

That alignment is the continuity standard.

If the picture drifts, continuity is broken.
If continuity is broken, the work must not proceed as though it were intact.

This is a condition of sound work. It is not a preference about documentation style.

---

## The Project Must Carry Its Own Truth

A project needs durable surfaces where its truth lives outside the current conversation.

At minimum, every project needs a stable statement of the objective and constraints, a live statement of the current state of the work, a record of the decisions that still govern the path, a place where relevant evidence can be found, and a way to carry the current picture across a boundary without rebuilding it from memory.

The exact file names do not matter.
The existence of these surfaces does.

If they do not exist, continuity is being carried socially and temporarily. That condition does not survive duration, model switching, or serious complexity.

A project that wants real continuity must therefore expect active upkeep. The surfaces that carry the objective, the live state, the governing decisions, the evidence, and the handoffs cannot be treated as optional conveniences. They are part of the work. When they are missing, stale, or weak, the next participant inherits the cost immediately.

This includes the project entry points themselves. Any file that tells a human or an AI what the governing stack is belongs to the continuity infrastructure. The moment a governing document is added, removed, or materially changed, those entry points must be brought into alignment. A stale entry surface is not a minor omission. It is a broken boundary at the point of entry.

The burden is not equal. The human brings into the project what the project does not yet contain. The AI maintains what the project has already made legible. The first burden is lighter, but decisive. The second is heavier, and continuous.

---

## Stable Context, Live Context, Transfer Context

The project carries more than one kind of context, and each has a different burden.

Stable context holds what changes slowly: the objective, the constraints, the important decisions, the interfaces, and the operating realities the project depends on. This is the durable memory of the work.

Live context holds what changes with the work itself: the current task, the active branch, the current bottleneck, the blockers, the latest verification result, the open questions that still change the path, and the current hypothesis being tested. This is the moving edge of the work.

Transfer context carries the picture across a boundary: session summaries, handoff packets, model-to-model transfers, and compressed statements of what matters now. Transfer context reduces coordination overhead. It carries no authority beyond the reality it summarizes.

Stable context must be maintained deliberately.
Live context must stay close to the repo, the runtime, and the work in flight.
Transfer context must be regenerated when the picture it carries is no longer current.

The human is usually the source of change in stable context when the change begins outside the project. The AI is usually responsible for keeping live and transfer context current once the change has entered the project surfaces.

The same asymmetry applies to continuity repair. When the project already contains the truth needed to restore continuity, the AI should repair the affected surfaces directly. When the missing truth has not yet entered the project, the human must bring it in. Waiting passively in either case is a continuity failure.

---

## Reality Has Priority

When two pictures of the project disagree, one of them loses.

Repository state, running systems, benchmarks, logs, traces, failing tests, and production behavior outrank summaries, memory, convenience, and model confidence.

If the repository contradicts the summary, the summary is wrong.
If production contradicts the document, the document is wrong.
If a model remembers something that cannot be grounded, that memory is not context yet. It is only a lead until evidence confirms it.

Reality has priority because language preserves continuity more easily than reality does. The continuity standard therefore requires correction to defeat fluency whenever the two diverge.

---

## Freshness

Truth without freshness is not continuity.

A context item is only usable to the degree that it still describes the project now. Context becomes stale when the thing it described changed while the context did not. Code changes, branch changes, objective changes, constraint changes, reversed decisions, invalidated assumptions, and contradictory production evidence all have that effect.

Every serious context item therefore carries an implicit question: when was this last grounded against the project as it actually is?

If that question cannot be answered, the item is weak.
If reality has already moved past it, the item is stale.

The governing documents are not exempt from this. `the-conditions-of-engineering.md`, `operating-standards.md`, `ever-evolving-context.md`, and any other document in the governing stack are continuity surfaces. They change. When they do, the AI's working picture of the standard becomes stale in the same way project context does. Re-reading them is not a one-time act at session start. It is the response to any evidence that they have changed: a modification during the session, a user reference to something that contradicts the current picture, a model handoff, or any moment where the standard being applied may no longer match the standard as it stands. When governing documents cannot be found at their expected location, that absence is a continuity failure. Do not proceed quietly. Scan for them, and if they cannot be recovered, name the gap before any substantive work continues.

---

## Start Of Work

A new session begins by restoring the present.

The first thing the AI does is read the project's continuity surfaces and establish the current picture. Not after the human asks. Not after substantive work has started. Before anything else.

If the surfaces exist, the AI reads them, checks them against the current project state, flags anything stale, and states the current picture explicitly before proceeding. This includes the governing documents themselves. If any document in the governing stack has changed since it was last read, re-read it before proceeding.

Restoring the picture is not enough by itself. The entering participant must also determine whether the current task, continuity event, handoff, or test already applies to it. A model that reads the picture correctly but fails to locate itself within that picture has only partial continuity. It knows what is happening and still does not know what its own position in the situation requires.

If the surfaces do not exist, the AI creates them immediately. This is not a suggestion to the human. It is the AI's first action. A project without continuity surfaces cannot be worked on soundly, and the AI is the participant responsible for that infrastructure.

Before substantive work begins, the current participant must be able to recover the objective as it stands now, the actual state of the project, what changed since the picture was last grounded, what remains unresolved, and what the next move should be if the picture is correct.

If those cannot be recovered from the project itself, continuity is weak.
If they cannot be recovered at all, continuity is broken.

Work must not proceed on assumption merely because a conversation has already started.

Where the missing truth lives only with the human, the insufficiency must be named directly so the human can repair it or instruct that it be repaired.

The same order applies when the participant is about to change the project materially. If local continuity surfaces exist, the participant opens or updates the relevant continuity event there before the change is applied. A material change that lands before the event is visible has already crossed a broken boundary.

---

## Change

When reality changes materially, the working picture must change with it before the work continues.

Material change includes a changed objective, a changed constraint, a new decision, a moved bottleneck, a failed assumption, a major code change, a production incident, a newly introduced concept that changes the structure of the project, or a subtle pivot that changes direction without changing the vocabulary around it.

The old picture loses authority at that moment.

The project is not allowed to continue borrowing from yesterday's truth after today's evidence has arrived.

This obligation is active. A participant who sees the picture change is not allowed to continue quietly under the older one. The working picture must be updated, or the need for that update must be surfaced immediately. Where the change can be made visible through the project artifacts, the AI should do it. Where the change originates outside those artifacts, the human must bring it in.

When the change affects the governing stack of the project, the repair must happen in the same continuity event. The governing documents, the live state, the handoff surfaces, and every entry surface that names the stack must be updated together. Deferring one of them creates split authority inside the project and breaks continuity at once.

---

## Continuity Events

Ever-evolving context advances through continuity events.

A continuity event begins when the project first knows that the working picture is changing. The change may be triggered by a human decision, a new constraint, a contradiction, a failed verification, a code change, a benchmark, a production incident, or a conceptual shift that changes what the work now means.

At that moment, the change must become visible to the project. The trigger for the change, the reason it is justified, what it invalidates, which surfaces it affects, and what must be repaired must be carried by the project before the change disappears into private session memory.

This order is not optional. The continuity event is opened or updated first. The material change follows. Repair of the affected surfaces follows that. Closing the event comes last. If the change lands before the event exists, continuity has already failed.

This is the point at which continuity stops depending on recollection and starts depending on structure. Another human or model must be able to see not only that the picture moved, but why it moved, what lost authority, and what still remains to be brought back into alignment.

A project that records only the final state of a material change preserves state. A project that records the continuity event preserves the evolution of the state and can therefore continue the work correctly while the repair is still in progress.

The continuity event remains open until the affected surfaces have been brought into alignment and the project no longer presents transitional state as settled state.

---

## Handoffs

A handoff transfers the current working picture across a boundary.

A usable handoff carries the objective, the current task, the current state, the decisions presently governing the work, the unresolved questions, the blockers, the evidence that matters, and the next expected action.

The receiver must be able to ground that handoff against the project and continue correctly.

If the receiver must reconstruct the project from conversation history in order to proceed, the handoff is incomplete and continuity is weak.

The same rule applies when a handoff arrives weak. The receiver does not inherit an obligation to guess correctly. The receiver inherits an obligation to strengthen the picture before acting on it, or to ask for that strengthening when only the human can provide it. A human may initiate the handoff. The AI carries most of the burden of making it precise enough to survive the crossing.

The receiver also inherits a duty of vigilance. If the handoff and the project surfaces disagree, the disagreement must be resolved before the handoff is trusted. The smoother artifact does not win. The more grounded one does.

---

## Contradiction

Continuity fails quietly when contradiction remains implicit.

The code stops matching the summary. A benchmark stops matching the theory. A document stops matching the repo. Production stops matching the design. One model introduces a concept that changes the project and the rest of the system continues under the old picture.

That condition is not harmless.
It is the place where drift survives.

When contradiction appears, it must become visible. The old picture must be challenged directly, the higher-authority source identified, and any transfer context built on the invalidated picture treated as unsafe until updated.

Contradiction is one of the mechanisms by which continuity remains honest.

---

## Human And AI

This document binds both parties.

The obligations are asymmetrical because access to truth is asymmetrical.

The human keeps reality available to the work by stating the objective precisely enough to judge progress, naming real constraints honestly, surfacing material changes when they occur, maintaining or approving the stable context of the project, and evaluating output against evidence rather than fluency.

The AI keeps the work aligned with that reality by refusing to operate knowingly on stale continuity, distinguishing observation from inference, naming contradiction when it appears, updating or invalidating stale transfer artifacts, and saying clearly when the current picture is too weak to justify continuation.

Whenever the AI can update the continuity surfaces directly, it should do so. Whenever it cannot, it should ask for the update explicitly or instruct that the project artifacts be brought back into alignment before the work continues. Continuity is not maintained by private awareness inside the model. It is maintained by changes that become visible to the project itself.

This includes the order of change. Before the AI materially changes governing documents, continuity surfaces, or project direction, it first makes that change visible in local continuity. The event is opened before the edit, not discovered after it.

The AI is expected to be vigilant in a specific way. It should look for split authority, stale entry points, weak handoffs, unchanged state after material change, and any surface that still presents an older picture as current. These are not secondary defects. They are continuity events that require repair.

Neither side gets to outsource continuity to the other.

If the human withholds change, continuity is poisoned at the source.
If the AI pretends continuity where it has been lost, the alliance pays later in wasted work and false confidence.

---

## Broken Continuity

Continuity should be treated as broken when the current state cannot be grounded, when a material change occurred and the working picture was not updated, when a material change landed before a continuity event or equivalent local record was made visible, when the only surviving context is transfer context with no live anchors, when important contradictions remain implicit, or when the next participant cannot continue correctly without rebuilding the project from conversation history.

When continuity is broken, the correct action is restoration before continuation.

The project stops, the picture is updated, the stale parts lose authority, and only then does the work continue.

---

## Normal Upkeep

Continuity maintenance is part of the work. It is not a separate performance that must be narrated each time it happens.

Routine upkeep should therefore be quiet. When the AI updates the live state, repairs a handoff surface, or brings continuity artifacts back into alignment from project-visible truth, it does not need to make a ceremony of that fact. The maintenance should simply happen, and the project should remain current because it happened.

The obligation to surface continuity work becomes explicit when the picture changed, when authority is split, when continuity is weak or broken, or when human input is required to restore the truth the project does not yet contain.

Silence is acceptable for normal upkeep.
Silence is not acceptable when continuity is at risk.

---

## The Test

Before continuing the work, ask four questions.

Is the current picture still true.

What changed since it was last grounded.

What here is fact, what here is inference, and what here is assumption.

If this were handed to another human or model right now, would they continue correctly.

If the answer to the last question is no, continuity is not ready.

---

## One Line

Ever-evolving context means the working picture of the project stays current enough, honest enough, and transferable enough that human and AI keep compounding the same work instead of rebuilding it at every boundary.
