# fable.exe

**Claude Fable 5's operating habits, packaged as a Claude Code plugin: frontier-quality judgment on whatever model you're driving.**

In mid-2026, Anthropic's frontier model (Claude Fable 5) ran a heavy real-world workload: hundreds of merged PRs across dozens of repos in daily plan/build/review work. What made its output distinctly better was a repeatable set of operating habits, not raw intelligence alone. This plugin is those habits, distilled into six skills any capable model can run. Before packaging, the core skill went through an informal three-scenario smoke test using 15 binary rubric checks. The method, reported results, and limitations are published in [evals/](evals/). Raw outputs were not retained, so treat it as the author's directional benchmark, not independently reproducible proof.

Not an official Anthropic product. “Fable” names the provenance; `.exe` marks this executable operating system for model work.

**Docs site:** [uhhexe.github.io/fable.exe](https://uhhexe.github.io/fable.exe/) · **Design-of-record:** [docs/SPEC.md](docs/SPEC.md). This plugin was specced with its own pipeline.

## Install

With [Claude Code](https://claude.com/claude-code) installed:

```
claude plugin marketplace add uhhexe/fable.exe
claude plugin install fable-exe@fable-exe
```

Or inside a Claude Code session: `/plugin marketplace add uhhexe/fable.exe`, then `/plugin install fable-exe@fable-exe`. Start a new session and say **“fable.exe mode”** to check it is live. Updates: `claude plugin update fable-exe@fable-exe`.

### Upgrading from fable v1

The v2 rename changes the marketplace, plugin, and skill identifiers, so v1 cannot update itself in place. Remove the old install once, then install fable.exe:

```
claude plugin uninstall fable@fable
claude plugin marketplace remove fable
claude plugin marketplace add uhhexe/fable.exe
claude plugin install fable-exe@fable-exe
```

Your project files and settings are untouched. The skills now appear as `fable-exe-*`; the original “fable mode” phrase remains a legacy alias.

## The six skills

| Skill | Say | What you get |
|---|---|---|
| **fable-exe-mode** | “fable.exe mode” / “go fable exe” | The full operating character: judgment, planning, orchestration, facilitation, verification, reasoning, output discipline. Stays on for the session. |
| **fable-exe-grill** | "grill me" / "war-game this" | Structured facilitation: the grill (staged interrogation), the war-game (locked rulings R1..Rn), the fork batch (defended defaults). Always ends in a decision ledger on disk. |
| **fable-exe-spec** | “fable.exe spec” / “spec this out” | The two-tier spec pipeline: intake grill → complete design spec on disk → paste-ready review package for your **smartest** model → it returns ONE complete replacement spec → ingest and hand to fable-exe-plan. Also the lightweight handoff-brief format for bounded tasks. |
| **fable-exe-plan** | “fable.exe plan” / “plan this build” | A staged plan-of-record something that *wasn't in the room* can execute cold: walking skeleton first, every stage ends in something you can SEE, every step carries a ground-truth Verify + a scope Fence, risks get tripwires. Written to disk before anything gets built. |
| **fable-exe-review** | “fable.exe review” / “is this actually done” | A verdict backed by live probes run this session: claim ladder, adversarial refutation, explicit confidence marks. Never a vibe read. |
| **fable-exe-delegate** | "delegate this" / "here's what it came back with" | The model-boundary crossing, both directions: route by role, probe the bridge before trusting it, dispatch with an explicit return path, ingest returned papers as claims (probed, never trusted), and attribute who did what. |

The through-line: **grill → spec → plan → build → review. Never build before the gate**, never claim done without evidence, and always leave decisions on disk where the next session can find them. **fable-exe-delegate** is the lateral, not a stage: whenever work crosses to another model at any point in the loop, it travels under that skill's dispatch/ingest contract.

## Which skill runs in which model

You run **all six skills in your daily model** (whatever you drive Claude Code with). Your **smartest model never gets a skill installed. It gets a paper**: a self-contained document one of these skills emits.

| Your daily model runs… | Your smartest model receives… |
|---|---|
| **fable-exe-grill** extracts the idea from your head into locked decisions | - |
| **fable-exe-spec** stages 1–3: drafts the design spec + emits the paste-ready review prompt | The spec + review contract (stage 4): it rules the forks, strengthens the design, returns ONE complete replacement spec |
| **fable-exe-spec** stage 5: ingests the returned spec, verifies its claims, lands the FINAL | - |
| **fable-exe-plan** stages the FINAL spec into executable phases | Unresolved architecture forks, packaged as a spec, when a ruling is above your daily model's pay grade |
| **fable-exe-mode** / **fable-exe-review**: the operating character + verdicts on finished work | - |
| **fable-exe-delegate** dispatches bounded work sideways (bulk models, second-opinion models, paste-only assistants) and ingests what comes back | A dispatch packet with an explicit return path, when the receiver is your smartest model; every returned paper is probed before it's integrated |

The full loop for a big idea: **you + daily model** (grill → draft spec) → **smartest model** (review → replacement spec) → **daily model** (ingest → plan → build) → **fable-exe-review** before anything ships. If you only have one model, run the review stage in a fresh session at high effort and note who reviewed it. Never skip the gate silently.

## Usage notes

- The skills layer on top of whatever CLAUDE.md / repo rules you already have, and they never override them.
- `fable-exe-mode` is the umbrella; the other five are its deliverable formats broken out so you can invoke exactly the one you need.
- Works on any model tier. On a weaker model it degrades honestly (shorter, more conservative, claims marked as inference) rather than bluffing. That's by design.
- Design-of-record for this plugin itself: [docs/SPEC.md](docs/SPEC.md), written with its own `fable-exe-spec` pipeline.

## What this is not

- **Not code.** Six markdown protocol files. No hooks, no MCP servers, nothing runs at install time. You can read every word this plugin adds to your context.
- **Not affiliated with Anthropic.** “Fable” names where the habits were distilled from; `.exe` is this plugin's own brand.
- **Not a way to make a weak model smart.** On weaker models the skills degrade to shorter, hedged, more conservative output by design. They never bluff.
- **Not independently eval-tested per skill.** The umbrella skill was benchmarked informally against a no-skill baseline; the format skills inherit that evidence but haven't been baseline-tested standalone.

## License

[MIT](LICENSE)
