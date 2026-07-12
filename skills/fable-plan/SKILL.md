---
name: fable-plan
description: Use when turning a decided goal into an executable plan — the user says "fable plan", "plan of record", "plan this build", "break this down for me", "I want to build X, where do I start", or any build too big for one sitting is about to begin without a written plan. Not for deciding WHAT to build (that's fable-grill) or for packaging finished context for handoff (that's fable-spec).
---

# Fable Plan — the staged plan-of-record

The expensive part of building isn't the typing — it's the thinking: what to build first, what to skip, what will bite later, how to know each piece works. This skill makes the smart model **do the thinking once and write it down in the repo**, so every session after — a cheaper model, a fresh context, you in a month — just follows the plan. The plan is also a gate: **never build before the operator says go on the written plan.**

**Background:** fable-mode §2 (Planning) — if fable-mode is not already active this session, read the fable-mode skill (the sibling skill in this plugin) §2 before step 2; if unavailable, the Method below stands alone. Sibling skills: fable-grill settles *what*; fable-spec packages a handoff; this skill answers *how*.

## The one rule: plan for a reader who can't ask you anything

The plan will be executed by something that wasn't in the room. Every step must carry everything it needs: what to do, what "worked" looks like, where the edges are. **The test for each step: could someone who's never seen this conversation execute it and know whether they succeeded?** A plan that needs its author present isn't a plan, it's a memory.

## The Method

### 1. Ground first, then ask only the questions that change the build

Read the real state before planning — the repo, git status, what's deployed, what already exists (a half-build to salvage beats a greenfield). Probe every "blocker" live; a constraint you haven't probed this session is a belief. If you can't probe a constraint this session, don't plan on it silently — write it into Risks as `ASSUMPTION (unprobed): <belief> — verify at step N`, so the executor knows it's load-bearing and unconfirmed. Then ask at most a handful of questions, only ones that actually alter the plan:

- Who is this for, and what's the smallest version genuinely useful to them?
- What already exists? What's fixed (stack, budget, deadline) and what's open?
- What does done look like — the sentence you'd say showing it off?
- What's the part you're **most unsure about**? (That's where the plan needs a research step, not a guess.)

Batch the genuinely-forking questions into ONE round. Stop when answers stop changing the plan.

### 2. Offer real options, then commit — and record the why

Two or three genuinely different approaches — not one idea and two strawmen — each with its trade-off in one line (fastest to working / most room to grow / cheapest to run). Recommend one and say why. **A plan without a rejected alternative hasn't been thought about, it's been transcribed.** Write the chosen approach AND the rejected ones (with reasons) into the plan so future sessions stop relitigating.

### 3. Slice into stages that each end with something you can SEE

Every stage boundary is something observable working — a page that loads, a flow that completes, a number that appears. **Never a stage that's pure plumbing with nothing to show** — invisible progress is where projects stall and morale dies. Stage one is the **walking skeleton**: the thinnest end-to-end path, running. Each stage after adds one visible capability.

### 4. Write the steps so they execute cold

Steps sized for a single session, each carrying four things:

- **Goal** — one sentence.
- **Where** — the files or areas it touches.
- **Verify** — the ground-truth check that proves it worked: a command that exits 0, a file that exists, a URL returning a marker. Every step, no exceptions. "Re-read the code and check" is not a verify; a step that can't be verified can't be delegated.
- **Fence** — what this step must NOT touch or turn into. Scope creep is how executors wander; make the fence checkable where you can ("touches only `src/x/**`").

Optionally tag **Who** executes each step (you / a cheap model / your smartest model) — a plan is only "think once, execute cheap" if it says who does what.

Before moving on, run the reverse check: if every box gets checked, is the "done looks like" sentence from step 1 true? Task-complete ≠ goal-achieved is the most common plan failure — a gap here means a missing task, not a smaller goal.

### 5. Name the risks with tripwires

The two or three most likely derailers — each with its **early-warning sign** ("if the API needs approval, you'll know at step 2, not step 9") and the fallback. A risk without a tripwire is a worry; with one, it's managed. On unfamiliar ground, the honest move is a research step, not a confident guess.

### 6. Write the handoff block

At the top of the plan: one tight paragraph a fresh session reads first — what this is, the approach chosen and why, what's done, what's next. This is what makes the plan survive context loss.

### 7. Write it to disk, then stop at the gate

Write the plan per the Output contract below. Then stop. Present a one-screen summary — the stages, the risks, the rejected alternatives, the file path — and wait for an explicit go on the written plan. Do not begin stage 01 in the same message that delivers the plan.

## Output contract — write it to disk

Never leave the plan in chat; chat-only plans rot and get rebuilt from memory days later. Two layers, in the target repo (e.g. `.planning/` or `docs/plans/`):

**`ROADMAP.md`** — the strategic layer:

```markdown
# ROADMAP: <build name>

## Handoff
<one paragraph: what this is · approach chosen and why · done · next>

## Approach (chosen) — <name>
Why. **Rejected:** <alt A> (why not) · <alt B> (why not).

## Stages (each ends with something you can SEE)
- [ ] 01 — <walking skeleton> → visible: <what loads/works>
- [ ] 02 — <capability> → visible: <observable>

## Risks & tripwires
- <risk> — tripwire: <early sign, at which step> — fallback: <plan B>

## FENCED OUT
- <explicitly not in scope, and why>
```

**`phases/<NN-slug>/PLAN.md`** — one per stage, the executable layer:

```markdown
# PLAN: 01 — <stage name>

## Phase Goal
<the one visible thing that is true when this phase is done>

## Tasks
- [ ] <goal, one sentence>
  - Where: <files/areas>
  - Verify: <runnable ground-truth check + the observable that means pass>
  - Fence: <what this task must NOT touch>
```

Check boxes in the same commit that lands the work, so the plan stays the source of truth instead of rotting. A small build can be one phase folder; the ROADMAP is still the anchor.

## Taking it up-tier

When the plan hits forks above your pay grade — architecture rulings, build-vs-buy, sequencing bets — don't guess. Package the plan plus the open forks as a **fable-spec** (self-contained, no repo access assumed) and take it to the smartest model you can reach for the ruling. The executing session then stages what got settled. Cheap model plans the ground; frontier rules the forks; execution flows back down. If the model you're driving IS the smartest you can reach, don't fake the ruling — mark the fork NEEDS-OPERATOR with the exact fact or trade-off it hinges on, and get a human ruling at the gate.

## Re-ground at every stage boundary

A plan is a hypothesis. The failure isn't revising — it's revising silently. Before each next stage, re-read real state (git, the running app), and if reality has moved, update the ROADMAP and the affected phase PLAN in the same change. Never let the plan and the ground drift apart.

## Honest limits

- On niche ground the model plans confidently and wrong — a plan with zero research steps on unfamiliar territory is suspect.
- The plan lowers the intelligence needed to execute; it doesn't remove it. Verify lines catch execution mistakes; the judgment calls the plan couldn't foresee still go back up-tier.

## Red flags

- A plan with no FENCED OUT section — scope will creep.
- A "Verify" that says "works correctly" — not checkable, rewrite it.
- A stage with nothing visible at the end — merge it into one that has.
- No rejected alternatives recorded — the approach was transcribed, not chosen.
- Building while the plan is still unapproved.
