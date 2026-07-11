---
name: fable-plan
description: Use when turning a decided goal into an executable plan — the user says "fable plan", "plan of record", "plan this out", "how should we build this", or any multi-step build is about to start without a written plan. Not for deciding WHAT to build (that's fable-grill) or for handing finished context to someone else (that's fable-spec).
---

# Fable Plan — the plan-of-record

Produces ONE approved plan a zero-context executor (a cheaper model, a future session, a collaborator) can run cold. The plan is a gate: **never build before the operator says go on the written plan.**

**REQUIRED BACKGROUND:** fable-mode §2 (Planning) — this skill is that section as a procedure with an output contract.

## Procedure

1. **Ground first.** Read the real state before planning: git status, what's deployed, what already exists in the repo, prior decisions on disk. A plan built on remembered state instead of read state is malpractice. Probe every "blocker" live — a constraint you haven't probed this session is a belief.
2. **Plan backward from the goal.** Write "what must be true when this is done" first. Derive tasks from that. Then run the reverse check: if every task completes, is the goal achieved? (Task-complete ≠ goal-achieved is the most common plan failure.)
3. **Every task names its verification.** Each task's "Done when" opens with a machine-checkable line (a command, a URL that renders, a file that exists). A task with no way to prove it landed is a hope, not a task.
4. **Sequence by the dependency spine.** The enabling primitive (shared schema, registry, component) lands first — every later task gets cheaper the moment it exists.
5. **Enumerate the cheap option first** for any new dependency/secret/service: (1) reuse existing stack, (2) cheap-and-local, (3) new integration. Heavier only wins with a written capability gap.
6. **Fence what's OUT.** An explicit FENCED OUT list, as loud as the task list.
7. **Name adoption.** When does this enter the operator's actual day, and what signal proves it did? Built-but-unadopted is not done.
8. **Write it to disk** in the target repo (e.g. `.planning/` or `docs/plans/`), then present for the go/no-go. Check boxes as work lands.

## Output contract

```markdown
# PLAN: <short name>

## Goal (what must be true when done)
<1-3 sentences, testable>

## Grounding (verified this session)
<what was read/probed, with the one-line evidence>

## Tasks
- [ ] 1. <task> — Done when: `<machine-checkable check>`
- [ ] 2. ...

## FENCED OUT
- <explicitly not in scope, and why>

## Adoption signal
<the moment this enters real use + the proof>

## Open forks
| Fork | DEFAULT (ruling + why) | or NEEDS-YOU: <missing fact> |
```

## Red flags

- A plan with no FENCED OUT section — scope will creep.
- A "Done when" that says "works correctly" — not checkable, rewrite it.
- Planning around a blocker nobody probed this session.
- Starting to build while the plan is still unapproved.
