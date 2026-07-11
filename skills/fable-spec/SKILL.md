---
name: fable-spec
description: Use when work must be handed to someone or something with zero context — the user says "fable spec", "write the spec", "make a brief", "hand this off", delegates a task to another model/session/collaborator, or asks to capture a design so anyone can pick it up later.
---

# Fable Spec — the self-contained handoff brief

Produces a **paper**: a self-contained artifact readable with zero conversation context. The test: could a stranger (or a fresh session, or a cheaper model) execute from this document alone, with nothing else from this conversation? If not, it's not a spec yet.

**REQUIRED BACKGROUND:** fable-mode §3 (Orchestration) — the brief skeleton and "papers are claims" doctrine come from there.

## The skeleton (every handoff unit, no exceptions)

```markdown
## Goal
<one sentence — what the receiver must make true>

## Context
<the minimum a stranger needs: what exists, what was decided, why. High-context and SHORT beats a wall of text.>

## Key files
<exact paths, what each is>

## Constraints
<owned file globs, what must NOT be touched, conventions to match>

## Done when
<machine-checkable line FIRST, then any judgment criteria>
```

Identical shape for every unit in a batch — the receiver should never have to guess the format.

## For bigger handoffs, add

- **Mission** — the larger why, one paragraph.
- **Ground-truth seed** — the verified facts this spec stands on, each with its evidence ("checked X this session: Y").
- **Johari 4-quadrant** — known-knowns (verified), known-unknowns (named open questions), unknown-knowns (things already built/decided that the receiver might rebuild — probe the repo for these), unknown-unknowns (the angles nobody has examined; name the gap-scan done).
- **Guardrails** — what the receiver must stop and ask about rather than decide alone.
- **Return contract** — the receiver comes back with a paper: goal, what was done, evidence, open items, next executable action.

## Rules

- **As-if-final.** No "as discussed above", no references to this conversation, no model-specific instructions. Commit the spec into the target repo so it survives the session.
- **Tight beats long.** Every model underperforms on huge prompts. Cut anything that doesn't change what the receiver does.
- **Received papers are claims, not truth.** When the work comes back, probe the load-bearing claims live before integrating.

## Red flags

- The spec references "the conversation" or "as we said" — it will die outside this session.
- "Done when" starts with a judgment call instead of a check.
- Context section longer than one screen — you're transcribing, not distilling.
