---
name: fable-spec
description: Use when a big idea needs to become a complete, build-ready design spec — the user says "fable spec", "spec this out", "full spec", "run the spec pipeline" — or when work must be handed to someone or something with zero context ("write the brief", "hand this off"). Also use when the user pastes back a reviewed spec from their smartest model ("here's the spec back") — that's INBOUND mode.
---

# Fable Spec — the two-tier spec pipeline (and the handoff brief)

Two jobs, one skill: turn a big idea into a **frontier-grade build spec** via a review round-trip, and package any work as a **self-contained paper** a stranger could execute cold. The core principle for both: **the artifact must survive outside this conversation** — no "as discussed above", no context the reader doesn't have, and always on disk the moment it exists (chat-only specs rot).

**REQUIRED BACKGROUND:** fable-mode §3 (Orchestration). Siblings: fable-grill runs the intake; fable-plan stages the finished spec into phases.

## The pipeline — who runs what

| Stage | Runs in | What happens |
|---|---|---|
| 1 · Intake grill | Your daily model + you | Extract everything: who it's for, every function, preferences and taste, what already exists, constraints, the north-star sentence |
| 2 · Draft spec | Same session | The complete design spec, self-contained, written to disk |
| 3 · Frontier package | Same session | A paste-ready review prompt with the contract embedded |
| 4 · Review & finalize | **Your smartest model** (fresh session, assume no repo access) | Rules the open forks, strengthens the design, returns ONE complete replacement spec |
| 5 · Ingest & route | Your daily model | Diff, verify claims, land the FINAL, hand to fable-plan |

The smartest model never receives a skill — it receives the paper stage 3 emits. **Never build from the unreviewed draft; the review gate is the point.** No stronger model available? Run stage 4 in a fresh session at deliberately high effort and stamp the spec with who reviewed it — never silently skip the gate.

### Stage 1 — Intake grill

Run the fable-grill format on the idea: staged interrogation, one theme at a time, decisions read back and locked. Exit when new questions stop changing the spec.

### Stage 2 — Draft spec

```markdown
# <Idea> — design spec, for review
*Self-contained: written for a reviewer with no repo access and no conversation context.*

## 0 · The spine — the one question this design answers
## 1 · Known knowns — stated intent + what ALREADY exists (build ON, don't rebuild)
## 2 · Function-by-function map — every surface, its behavior, its states
## 3 · Design language & taste constraints (locked preferences from the grill)
## 4 · Open questions the grill couldn't close
## 5 · Open forks — one row each: DEFAULT (my ruling + why) or NEEDS-YOU (missing fact)
## 6 · FENCED OUT — loudly
## 7 · Acceptance — what must be observably true for v1 to be "done"
```

Write it to the repo (`docs/plans/YYYY-MM-DD-<slug>-spec.md`) or, with no repo, somewhere durable the user can reach.

### Stage 3 — Frontier package

Emit a sibling paste-ready prompt embedding this contract, and hand both to the user:

> You are the reviewer of record on the attached design spec. (1) Check it for coherence; flag anything unverifiable as NEEDS-PROBE rather than trusting it. (2) Rule every open fork in §5 — R1..Rn, each with the WHY. (3) Tweak, strengthen, and adjust anything needed to make this the highest-quality buildable spec — architecture, sequencing, scope, taste. (4) Return ONE COMPLETE REPLACEMENT SPEC (never a diff or commentary), same section structure, rulings applied inline plus a changelog. (5) No execution: do not write code or expand scope beyond the spec's north star.

### Stage 5 — Inbound ingest

When the user pastes the reviewed spec back: diff it against the draft and surface every ruling · verify the load-bearing claims against the actual project (the reviewer had no repo access — probe what it inferred) · land the result as `…-spec-FINAL.md` next to the draft · route ONE next action, almost always fable-plan. A finished spec that just sits is a failed run.

## The handoff brief (the lightweight format)

For delegating a bounded task rather than designing a system, skip the pipeline and emit the uniform skeleton — identical shape for every unit, so the receiver never guesses the format:

```markdown
## Goal        — one sentence: what the receiver must make true
## Context     — the minimum a stranger needs; short beats complete-transcript
## Key files   — exact paths, what each is
## Constraints — owned file globs, what must NOT be touched, conventions
## Done when   — machine-checkable line FIRST, then judgment criteria
```

For bigger handoffs add: mission (the larger why) · ground-truth seed (verified facts + their evidence) · guardrails (what the receiver must ask about rather than decide) · return contract (a paper: goal, what was done, evidence, open items, next action). Received papers are claims, not truth — probe before integrating.

## Red flags

- The spec references "the conversation" or "as we said" — it dies outside this session.
- Building from the draft because the review round-trip feels slow — that's the gate you're skipping.
- A fork table with no defended defaults — you're outsourcing thinking, not requesting review.
- The reviewed spec comes back and only gets read, not diffed and probed.
