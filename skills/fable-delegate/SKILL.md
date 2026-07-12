---
name: fable-delegate
description: Use when work is about to cross a model boundary in either direction — the user says "delegate this", "send this to my other model", "have <another assistant> do this", "farm this out", "run this on the cheap model", "get another model's take on this", or pastes back a delegate's output ("here's what it came back with", "it says it's done"). Also use when THIS session is handed a brief authored by another model or session ("another model sent this", "execute this brief"). Not for turning ideas into specs or the spec review round-trip (fable-spec), and not for in-session verdicts on finished work (fable-review).
---

# Fable Delegate — work crossing a model boundary, both directions

You are one model in a fleet: a daily driver, a smartest model, bulk models, second-opinion models, paste-only models. Work moves between them constantly, and the failures are rarely in the content — they're in the crossing: briefs that leave with no return path and rot, bridges that drifted and fail silently, self-reported "done" integrated on trust, deliverables stranded outside the shared repo. This skill owns the crossing. **fable-spec owns what goes in the envelope; this skill owns the postal system.**

**Background:** fable-mode §3 (Orchestration) — the sibling skill in this plugin; if unavailable, this file stands alone. Siblings: fable-spec provides the brief skeleton and the spec review round-trip (that round-trip is fully specified there — don't reroute it here); fable-review is the heavy verdict when inbound stakes justify it.

## 1 · Route — should this cross the boundary at all?

Roles, not names — resolve each to whatever the operator actually runs:

| Task shape | Role |
|---|---|
| Architecture rulings, design synthesis, plan authorship, taste-critical work that ships | **Keep it** — or take it UP to your smartest model |
| Bulk breadth: log digging, giant-doc reading, wide mechanical sweeps, fixture generation | **Bulk model** — cheapest that clears the bar |
| Independent second pass on a diff or decision | **Second-opinion model** — a different model family beats your own |
| Reasoning about a describable design, pattern, or market — no file access needed | **Paste-only model** works fine |
| Anything this session can already answer with evidence in hand | **Don't delegate** — the round-trip costs more than the lookup |

Judge the output, not the price: if a cheaper role's result misses the bar, redo it up-tier without asking. Delegating the judgment itself is the one move that never pays.

## 2 · Know the transport before you write a word

Three transports, in descending shared context: **subagent or fresh session** (may share a filesystem — still write for a cold start), **CLI bridge** (no conversation context, maybe repo access), **paste-only** (no context, no filesystem — the operator is the courier). The brief's self-containment level comes from the transport, so establish it first.

- **Probe a bridge before trusting it.** One real, non-mocked round-trip — a one-word ping — before the real dispatch, and verify every flag or option you pass against the tool's current help. CLI surfaces drift, and a drifted bridge fails every turn while looking configured.
- **Surface the substrate assumption before building any new bridge** — auth model, billing path, transport: "assuming subscription CLI, not API keys — say so if not." A wrong substrate assumption scraps the whole build.
- **Paste-only receivers get everything embedded** — file maps, signatures, data shapes — and told so: "you have no repo access; don't ask for files; reason from what's here." Keep it modest: models underperform on walls of text. Constraints live in the brief; the prompt stays small.
- **Paths travel badly.** Use repo-relative paths or state the machine assumption outright, and name a fallback access route (the shared remote) for when the primary is unreachable.

## 3 · Outbound — the dispatch contract

1. **Re-ground immediately before dispatch.** Facts move under pending artifacts — a premise written this morning can be false by afternoon. Verify the brief's premise against live state (git, the running thing), stamp it with as-of state, and check that no parallel lane already holds the work.
2. **Package with the fable-spec handoff skeleton** (Goal / Context / Key files / Constraints / Done when), and tag every input by authority so the receiver knows what it may touch: **VERIFIED** (probed this session, evidence named) · **RULED** (operator decision — do not relitigate) · **PRIOR-REVIEW** (another model's take — overturnable with evidence) · **CLAIMED** (a self-report — plausible, not true).
3. **Name the return path in the brief itself.** Who carries the reply back, the exact landing spot for the deliverable (a named file or branch in the shared ref), and the return shape — a paper: what was done, evidence, open items, next action. **A brief with no return path is a failed run before it leaves.**
4. **Track the pending.** Record the dispatch durably — a pending line in the repo, or wherever the operator tracks work — with a check-by time. Past that time, silence means FAILED, not in-progress.

## 4 · Inbound — ingest, never paste-and-trust

1. **Check for silent no-op and success theater first.** Does the deliverable exist where the contract said — the branch, the PR, the file? Zero output with no error is a failed dispatch that reads exactly like progress.
2. **A returned paper is claims, not truth.** Probe the load-bearing ones yourself: re-run the tests, hit the endpoint, read the file. Any claim from the party that built the thing stays unverified until independently re-run. Stakes high? Run the full fable-review.
3. **Sort the content:** **ADOPT** (sound, fits constraints — say what changes) · **CONTEXT-BLIND MISS** (wrong because the receiver couldn't see X — name the gap in one line) · **WORTH SURFACING** (a consideration nobody had weighed — the gold of second opinions).
4. **Land it.** Result committed to the shared ref, pending line flipped, ONE next action routed. Then report: what was delegated, what came back, what you verified versus took on trust.

## 5 · As receiver — when the brief comes TO you

1. **Probe the premises before building.** The sender's ground truth may already be stale — verify the claims that shape the work against live state. A false premise ("build X" when X shipped last week) means surface it, never build on it.
2. **Honor the authority tags.** RULED is ruled. Overturn PRIOR-REVIEW only with evidence.
3. **Land where the brief says.** Deliverables go to the named return path, committed to the shared ref — output sitting uncommitted on a local checkout effectively doesn't exist to the next session.
4. **Return a paper, rung-honest.** State the claim-ladder rung for every claim ("tests pass — run attached", never "verified" for a rung you didn't climb) and list what you did NOT check. Blocked? Say exactly why — a delegate that fails loud is worth ten that fail silent.

## 6 · Attribution

The final artifact says who did what: which role produced each piece, what was independently verified, what was integrated on trust and marked so. Never present a delegate's verification as your own.

## Degradation

On a weaker model this skill gets more conservative, never fancier: fewer simultaneous dispatches, every inbound claim held at PLAUSIBLE until probed, and the ingest judgment escalated up-tier rather than faked. The mechanical rules — named return path, ping-before-trust, premise probe, land-in-shared-ref — never shrink.

## Red flags

- A brief leaves without a named landing file or return carrier — it will rot.
- Integrating a delegate's work because "it says tests pass" — re-run them.
- A new bridge trusted without one real ping round-trip.
- A pending dispatch past its check-by time still described as "in progress."
- Executing a received brief whose premise you never probed against live state.
- The delegation invisible in the final report — the operator can't audit what was trusted.