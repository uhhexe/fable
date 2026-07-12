# fable: design spec (the plugin's own design-of-record)

*Built with the plugin's own `fable-spec` pipeline, because a plugin about specs should be able to spec itself. Self-contained: readable with no other context.*

## 0 · The spine: the one question this design answers

**How do you get frontier-quality output from whatever model you're driving? Habits, not model access.**

In mid-2026 Anthropic's frontier model (Claude Fable 5) ran a heavy real-world workload for one operator: hundreds of merged PRs, dozens of repos, daily plan/build/review/facilitation work. What made its output distinctly better was a repeatable set of operating habits, not raw intelligence alone: verdict-first judgment, goal-backward planning, evidence-before-assertion verification, orchestration of cheaper models, and structured facilitation that ends in decisions on disk. When the model was retired from that operator's router, the habits were distilled into a protocol any capable model can run. This plugin is that protocol, packaged for anyone.

## 1 · Known knowns: what this is built from

- **Provenance:** distilled from heavy daily frontier-model usage on a real workload, then preserved as the `fable-mode` skill; the core skill was informally eval-tested against a no-skill baseline before packaging (three scenarios, 15 rubric checks, 15/15 with the skill vs 13/15 without, one run on one model with automated grading). Spec, graded results, and limitations: [../evals/](../evals/). Treat it as the author's small-sample benchmark, not a proven result.
- **The decomposition:** one umbrella skill (the operating character) plus five deliverable formats broken out so each is independently invocable. Four were originally sections inside the umbrella; users reached for them by name, so they became skills. The fifth (`fable-delegate`, v1.3.0) was added from field evidence: two weeks of real usage showed 58 model-boundary crossings whose failures clustered at the crossing itself, which no existing skill owned.
- **The two-tier insight:** the highest-leverage workflow is not "run everything on the smartest model" but *daily model extracts and drafts; smartest model rules and finalizes; nothing gets built from an unreviewed spec.* The plugin encodes that round-trip explicitly (`fable-spec`).

## 2 · Function-by-function map

| Skill | Trigger phrases | Deliverable |
|---|---|---|
| `fable-mode` | "fable mode", "go fable", "frontier mode", output feels "junior/sloppy" | Session-wide operating character: judgment, planning, orchestration, facilitation, verification, reasoning, output discipline |
| `fable-grill` | "grill me", "war-game this", "what am I not seeing" | Decision ledger on disk, via the grill (staged interrogation), war-game (rulings R1..Rn), or fork batch (defended defaults) |
| `fable-spec` | "fable spec", "spec this out", "here's the spec back" | The two-tier pipeline: intake grill → self-contained design spec → review package for your smartest model → ingest its replacement spec as the FINAL. Also the lightweight handoff-brief format |
| `fable-plan` | "fable plan", "plan this build", "break this down" | Staged plan-of-record executable cold: walking skeleton, visible stage boundaries, Verify + Fence per step, risk tripwires, handoff block |
| `fable-review` | "fable review", "is this actually done", pre-merge | Evidence-backed verdict: claim ladder, live probes, adversarial refutation, CONFIRMED/PLAUSIBLE/SPECULATIVE marks |
| `fable-delegate` | "delegate this", "send this to my other model", paste-back of a delegate's output, this session receives another model's brief | The model-boundary crossing, both directions: route by role, transport-aware brief, explicit return path, inbound papers probed never trusted, attribution of who did what |

The intended loop: **grill → spec → (smartest-model review) → plan → build → review.** Never build before the gate. `fable-delegate` is the lateral, not a stage: work crossing to another model at any point travels under its dispatch/ingest contract.

## 3 · Design rules (locked)

- **Protocols, not personas.** No tone instructions, no roleplay, only decision procedures and output contracts. The mode shows in the work, not the narration.
- **Trigger-only descriptions.** Skill frontmatter describes *when to invoke*, never summarizes the workflow (agents shortcut descriptions that contain workflow).
- **Papers over conversations.** Every format's terminal deliverable is a self-contained artifact on disk. Chat-only output rots.
- **Generic by construction.** No references to any specific person's infrastructure, memory systems, or repos. "The operator" is whoever installed it.
- **Tier-portable with an honesty floor.** Any skill can land on a weak model; it must degrade to shorter, more conservative, explicitly-hedged output. Never bluff.
- **Layered, never overriding.** Skills sit on top of the user's CLAUDE.md and repo rules; nothing here supersedes them.

## 4 · Known unknowns

- The five format skills inherit the umbrella's eval evidence but have not been independently baseline-tested as standalone skills.
- Trigger-phrase collision with users' existing skills ("grill", "spec") is untested in the wild.

## 5 · Forks, ruled

| Fork | Ruling | Why |
|---|---|---|
| One plugin vs five | **One plugin, five skills** | They share one doctrine; installing partially breaks the loop |
| Five skills vs six (v1.3.0) | **Six: `fable-delegate` added** | Two weeks of field data (58 boundary crossings, ~4/day) showed failures cluster at the crossing itself (briefs with no return path, drifted bridges, self-reports integrated on trust) and no existing skill owned it; fable-spec owns the envelope, fable-delegate owns the crossing |
| Name: `fable-5-plugin` vs `fable` | **`fable`** | Matches plugin + marketplace name → cleanest install (`fable@fable`); "Fable 5" stays in the description as provenance |
| Include the captured Fable 5 consumer system prompt | **Excluded** | It's a prompt dump, not the operating character; adds 117KB of no-protocol content |
| Distribution | **Public GitHub repo as its own marketplace** | `claude plugin marketplace add uhhexe/fable`: zero packaging overhead, updates ship by push |

## 6 · FENCED OUT

- No execution skills. Building is the host session's job; this plugin shapes judgment and artifacts.
- No memory/infra integrations (Engram, vaults, task engines); those are operator-specific.
- No hardcoded model names in procedure text: "your daily model" / "your smartest model" are roles.
- Not an official Anthropic product; "Fable" here names the provenance, nothing else.

## 7 · Acceptance: v1 is done when

- `claude plugin validate .` passes clean.
- `claude plugin marketplace add uhhexe/fable` + `claude plugin install fable@fable` works on a machine that has never seen this repo.
- Each skill fires on its trigger phrases and produces its contracted deliverable shape.
- A session on a mid-tier model with `fable-mode` on produces verdict-first, evidence-marked output that survives the skill's own quick self-check.
