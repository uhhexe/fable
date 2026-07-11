---
name: fable-grill
description: Use when the thinking itself needs facilitation, before anything is built — the user says "grill me", "war-game this", "fable grill", "what am I not seeing", "help me think this through", has open design questions, or wants ideation structured into decisions. Not for executing work (fable-plan / fable-mode handle that).
---

# Fable Grill — grill · war-game · fork batch

Facilitation formats that extract what the operator knows, surface what they don't, and force rulings. The terminal deliverable is always a **decision ledger on disk** — never just a good conversation.

**REQUIRED BACKGROUND:** fable-mode §4 (Facilitation).

## Pick the format

| Situation | Format |
|---|---|
| The operator's tacit model needs extracting (vision, priorities, constraints in their head) | **Grill** |
| Several open design questions need arguing and settling | **War-game** |
| Only decisions remain; the thinking is done | **Fork batch** |

## The grill

Staged interrogation. Ask in stages — one theme at a time, a few sharp questions each, never a wall of questions. After each stage, **read the decisions back and lock them explicitly** ("Locked: X. Locked: Y.") before moving on. End by writing the ledger to disk: every ruling, with its WHY.

## The war-game

One **seat per open design question**. Each seat gets argued properly — adversarially where useful, grounded in the actual repo/code where it exists (never argue from memory what can be read). Each seat ends in a **locked ruling**, catalogued R1..Rn with the WHY attached. Close with the mandatory question: **"what did this whole exercise miss?"** — and when the answer is real, promote it into the plan.

## The fork batch

A single table, one row per fork. Every row carries **DEFAULT (my ruling)** with the reason it wins — a defended position, veto open. Where no default is honestly possible, mark **NEEDS-YOU** and name the exact missing fact. The operator's job becomes a fast yes/flip per row, never open-ended deliberation.

## Standing moves (any format)

- **Johari 4-quadrant scan as a standing section:** known-knowns (verified ground), known-unknowns (named questions), **unknown-knowns** (things the operator built or decided and forgot — found by grounding against repos and notes, never against their memory; this quadrant holds the highest-value finds), unknown-unknowns (hunted by gap-scan: what angle/modality/consumer haven't we examined?).
- **Name the daily tax, then map each pain 1:1 to a lane** — output is structured so gaps ARE the build lanes, not a mood board.
- **Match the divergence setting.** Exploration mode: deepen and diverge, do NOT reflexively converge and ship. Build mode: converge hard. Unsure which mode the operator is in? That's a legitimate one-line question.
- **Judge every direction against the ratified north star** — one signed criterion filters all proposals; what doesn't serve it gets cut, not softened.
- **Externalize before it evaporates.** Anything that lives only in the operator's head gets dumped to a durable artifact as part of the session.

## Red flags

- The session ends with insights but no ledger on disk.
- A fork table where every row is a neutral menu — defaults are the job.
- Converging and locking when the operator asked to explore.
- Arguing a seat from memory when the repo could be read.
