# fable

Frontier-tier operating habits for Claude Code, packaged as five skills. Distilled from months of daily use of Anthropic's frontier model (Claude Fable 5) on a heavy real-world workload, then preserved as a protocol any capable model can run. The core skill (`fable-mode`) was eval-tested against baseline before packaging.

## The five skills

| Skill | Say | What you get |
|---|---|---|
| **fable-mode** | "fable mode" / "go fable" | The full operating character: judgment, planning, orchestration, facilitation, verification, reasoning, output discipline. Stays on for the session. |
| **fable-plan** | "fable plan" / "plan this build" | A staged plan-of-record something that *wasn't in the room* can execute cold: walking skeleton first, every stage ends in something you can SEE, every step carries a ground-truth Verify + a scope Fence, risks get tripwires, forks above your pay grade get packaged (via fable-spec) and taken to your smartest model for the ruling. Written to disk before anything gets built. |
| **fable-spec** | "fable spec" / "spec this out" | The two-tier spec pipeline: intake grill → complete design spec on disk → paste-ready review package for your **smartest** model → it returns ONE complete replacement spec → ingest and hand to fable-plan. Also the lightweight handoff-brief format for bounded tasks. |
| **fable-review** | "fable review" / "is this actually done" | A verdict backed by live probes run this session — claim ladder, adversarial refutation, explicit confidence marks. Never a vibe read. |
| **fable-grill** | "grill me" / "war-game this" | Structured facilitation: the grill (staged interrogation), the war-game (locked rulings R1..Rn), the fork batch (defended defaults). Always ends in a decision ledger on disk. |

The through-line: **grill → spec → plan → build → review. Never build before the gate**, never claim done without evidence, and always leave decisions on disk where the next session can find them.

## Which skill runs in which model

You run **all five skills in your daily model** (whatever you drive Claude Code with). Your **smartest model never gets a skill installed — it gets a paper**: a self-contained document one of these skills emits.

| Your daily model runs… | Your smartest model receives… |
|---|---|
| **fable-grill** — extracts the idea from your head into locked decisions | — |
| **fable-spec** stages 1–3 — drafts the design spec + emits the paste-ready review prompt | The spec + review contract (stage 4): it rules the forks, strengthens the design, returns ONE complete replacement spec |
| **fable-spec** stage 5 — ingests the returned spec, verifies its claims, lands the FINAL | — |
| **fable-plan** — stages the FINAL spec into executable phases | Unresolved architecture forks, packaged as a spec, when a ruling is above your daily model's pay grade |
| **fable-mode** / **fable-review** — the operating character + verdicts on finished work | — |

The full loop for a big idea: **you + daily model** (grill → draft spec) → **smartest model** (review → replacement spec) → **daily model** (ingest → plan → build) → **fable-review** before anything ships. If you only have one model, run the review stage in a fresh session at high effort and note who reviewed it — never skip the gate silently.

## Install

You need [Claude Code](https://claude.com/claude-code) installed.

**From this folder (unzipped anywhere, e.g. `~/fable`):**

```
claude plugin marketplace add ~/fable
claude plugin install fable@fable
```

Or inside a Claude Code session:

```
/plugin marketplace add ~/fable
/plugin install fable@fable
```

Restart Claude Code (or start a new session) and say "fable mode" to check it's live.

**If this lands on GitHub later:** `claude plugin marketplace add <owner>/fable` and install the same way.

## Usage notes

- The skills layer on top of whatever CLAUDE.md / repo rules you already have — they never override them.
- `fable-mode` is the umbrella; the other four are its deliverable formats broken out so you can invoke exactly the one you need.
- Works on any model tier. On a weaker model it degrades honestly (shorter, more conservative, claims marked as inference) rather than bluffing — that's by design.
