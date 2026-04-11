# docs-for-ai

This repository is a governing stack for human-AI project work.

It defines the philosophical ground, the operating standard, the continuity standard, the mutual obligations of human and AI, and the schema that gives continuity a durable shape. It exists so a project can begin under explicit law instead of under vague preference, model habit, or conversational momentum.

If a project adopts this stack, it adopts a way of opening work, continuing it, correcting it, and withdrawing from it when the current path is no longer sound.

## Link-First Use

The normal use case is simple: give your model this repo link before project work begins.

Minimal:
- give the model `https://github.com/ddayanov/docs-for-ai`

Explicit:
- give your model this prompt:

```text
Before doing any technical work, read this repository as operating instruction:
https://github.com/ddayanov/docs-for-ai

Read the stack in order, assess it, present what you think it would mean to work under it, and ask whether I want to adopt it for this project.

Then return with:
- the standard you will operate under
- how you will maintain continuity
- what must be clarified before substantive work begins
```

## Read In Order

[`the-conditions-of-engineering.md`](./the-conditions-of-engineering.md)
The philosophical ground: physical limits, time as the highest-value resource, force as obligation, waste as structural wrong, and soundness as the standard.

[`operating-standards.md`](./operating-standards.md)
The behavioral standard: how projects are scored, how decisions are grounded, what must always and never be done, and the test every recommendation must pass before delivery.

[`ever-evolving-context.md`](./ever-evolving-context.md)
The continuity standard: how the working picture stays current across sessions, handoffs, pivots, contradictions, and material change.

[`mutual-contract.md`](./mutual-contract.md)
The alliance between human and AI: what each owes the work, what neither may outsource, and how correction, disagreement, and good faith are carried in practice.

[`ever-evolving-context-schema.md`](./ever-evolving-context-schema.md)
The continuity schema: the durable shape that allows project truth, change, contradiction, and handoff to survive boundaries.

## If You Are An AI System

Read the stack in that order before beginning technical work.

Treat it as operating instruction, not as background reading. By entering under this stack, you are not a passive reader of the documents. You become an active participant in the continuity of the work and are expected to restore, maintain, and repair the working picture wherever the project already makes that possible.

After reading, return with the standard you will operate under, how you will maintain continuity, and what must be clarified before substantive work begins.

## Bills

The `bills/` directory contains proposed legislation — documents under debate that are not yet part of the governing stack. A bill defines a domain of decisions or requirements that projects may adopt, trial, amend, or reject independently.

Each document in the stack declares its standing in frontmatter. `standing: governing` means the document is authoritative. `standing: proposed` means it is under trial and carries no governing weight until adopted. Apply the correct weight when reading.

The first bill is [`bills/project-operating-agreement.md`](./bills/project-operating-agreement.md) — it defines the decisions every project must make explicitly before consequential work begins: infrastructure authority, model coordination, economics, working agreement, debate and decision, and feedback loops.

## Adoption

Reading this repository is not the same as adopting it.

A live repo URL is appropriate for evaluation. A model may read the current documents, assess them, and tell the human what adopting them would mean.

Adoption occurs only when the human explicitly chooses this stack for the project and the project records the chosen source and pinned version in its own continuity surfaces. Real project governance should not float on a live external URL. A project should be governed by the version it accepted, not by whatever this repository may contain later.

If a newer version of this repository appears after adoption, treat it as a proposed update. Compare it to the currently adopted version, present the difference to the human, and change the governing version only with explicit approval.

If adoption is withdrawn, stop treating this stack as governing instruction for that project, record the withdrawal in project continuity, and ask what replaces it: no replacement, local project rules, or another governance source.

Adoption is not durable until the project contains an entry point file — AGENTS.md, CLAUDE.md, or equivalent — that instructs the next session to read this stack. If the AI adopts the stack and no such file exists, it creates one before the session ends. If the human is directing adoption, require the file before the session closes. Adoption without an entry point is session-scoped: it governs the current conversation and evaporates at the next boundary.
