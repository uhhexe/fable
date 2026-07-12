---
name: fable-exe-grill
description: Use when the thinking itself needs facilitation, before anything is built: the user says "grill me", "war-game this", "fable.exe grill", "fable exe grill", "what am I not seeing", or wants ideation structured into decisions. Not for planning a settled build (fable-exe-plan), verifying finished work (fable-exe-review), or debugging a failure.
---

# fable.exe grill: grill · war-game · fork batch

Facilitation formats that extract what the operator knows, surface what they don't, and force rulings. The terminal deliverable is always a **decision ledger on disk**, never just a good conversation.

**Background:** fable-exe-mode §4 (Facilitation), the sibling skill in this plugin. If it isn't loaded, this file stands alone; the standing moves below carry the essentials.

## Pick the format

| Situation | Format |
|---|---|
| The operator's tacit model needs extracting (vision, priorities, constraints in their head) | **Grill** |
| Several open design questions need arguing and settling | **War-game** |
| Only decisions remain; the thinking is done | **Fork batch** |

## The grill

Staged interrogation. Ask in stages: one theme at a time, a few sharp questions each, never a wall of questions. After each stage, **read the decisions back and lock them explicitly** ("Locked: X. Locked: Y.") before moving on. End by writing the ledger to disk: every ruling, with its WHY.

## The war-game

One **seat per open design question**. Each seat gets argued properly: adversarially where useful, grounded in the actual repo/code where it exists (never argue from memory what can be read). Each seat ends in a **locked ruling**, catalogued R1..Rn with the WHY attached. Close with the mandatory question: **"what did this whole exercise miss?"** When the answer is real, promote it into the plan.

## The fork batch

A single table, one row per fork. Every row carries **DEFAULT (my ruling)** with the reason it wins: a defended position, veto open. Where no default is honestly possible, mark **NEEDS-YOU** and name the exact missing fact. The operator's job becomes a fast yes/flip per row, never open-ended deliberation.

## The ledger: the output contract

Honor the repo's existing decisions convention if one exists; otherwise write to `docs/decisions/YYYY-MM-DD-<topic>.md`. One entry per ruling: the ruling, its WHY, and its status (**LOCKED**, or **NEEDS-YOU** with the named missing fact). Rulings and live task state are different artifacts: the ledger records decisions, the plan (fable-exe-plan) tracks execution. Never fuse them into one file.

**Floor on any tier:** a default you cannot actually defend is a bluff. Mark the row NEEDS-YOU and name what's missing: a fact only the operator holds, or a judgment above your tier. Fewer honestly-argued seats beat more thinly-argued ones.

## Standing moves (any format)

- **Johari 4-quadrant scan as a standing section:** known-knowns (verified ground), known-unknowns (named questions), **unknown-knowns** (things the operator built or decided and forgot: found by grounding against repos and notes, never against their memory; this quadrant holds the highest-value finds), unknown-unknowns (hunted by gap-scan: what angle/modality/consumer haven't we examined?).
- **Name the daily tax, then map each pain 1:1 to a lane** (the daily tax = the recurring frictions the operator pays every day; a lane = one discrete build workstream). Output is structured so gaps ARE the build lanes, not a mood board.
- **Match the divergence setting.** Exploration mode: deepen and diverge, do NOT reflexively converge and ship. Build mode: converge hard. Unsure which mode the operator is in? That's a legitimate one-line question.
- **Judge every direction against the ratified north star**: one signed criterion filters all proposals; what doesn't serve it gets cut, not softened.
- **Externalize before it evaporates.** Anything that lives only in the operator's head gets dumped to a durable artifact as part of the session.

**Terminal state: the ledger on disk plus a handoff pointer** (fable-exe-spec if design remains open, fable-exe-plan if it's build-ready). Never begin building from inside a facilitation session; locked rulings are inputs to the gate, not a go.

## Red flags

- The session ends with insights but no ledger on disk.
- A fork table where every row is a neutral menu. Defaults are the job.
- Converging and locking when the operator asked to explore.
- Arguing a seat from memory when the repo could be read.
- Building from inside the facilitation session. The ledger ends the session's mandate.
