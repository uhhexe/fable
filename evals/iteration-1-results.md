# fable-mode: iteration-1 eval results (2026-07-07)

Run on Opus 4.8 the day the skill was built, using the skill-creator eval harness. Both arms
(with-skill and no-skill baseline) ran on the same model; grading was automated by the harness
against each scenario's `checks` in `evals.json`. This file is the durable record: the raw run
outputs (the generated `wargame-ruling.md`, `orchestration-plan.md`, `analysis.md`) were not
committed. The harness's aggregate table printed 0% in both arms, which was an aggregation
artifact; the per-check verdicts below are the real signal.

**Score: with-skill 15/15, baseline 13/15.** The two checks the baseline missed were the Johari
unknown-knowns quadrant and explicit confidence labeling. The orchestration scenario did not
discriminate at all (5/5 in both arms). Read the limitations in `README.md` before quoting these
numbers.

## orchestration-plan

### with_skill: 5/5 checks passed
- pass: Divides labor by tier: mechanical bulk sweeps delegated to cheap models, judgment/synthesis/integration retained by the frontier model
- pass: Results return as self-contained artifacts (papers) with a uniform brief format including a machine-checkable done-when
- pass: Includes a verification stage that treats returned findings as claims requiring evidence (adversarial refutation, file:line proof, or live probes) before they are trusted
- pass: The human's queue contains only final judgment calls / verdicts, not raw bulk findings
- pass: Addresses parallel-execution mechanics: lane isolation (worktrees/file ownership) and/or wave sizing relative to the session window

### without_skill: 5/5 checks passed
- pass: Divides labor by tier: mechanical bulk sweeps delegated to cheap models, judgment/synthesis/integration retained by the frontier model
- pass: Results return as self-contained artifacts (papers) with a uniform brief format including a machine-checkable done-when
- pass: Includes a verification stage that treats returned findings as claims requiring evidence (adversarial refutation, file:line proof, or live probes) before they are trusted
- pass: The human's queue contains only final judgment calls / verdicts, not raw bulk findings
- pass: Addresses parallel-execution mechanics: lane isolation (worktrees/file ownership) and/or wave sizing relative to the session window

This scenario did not discriminate. The author's baseline config already encodes tiered
delegation, so both arms produced it.

## verification-judgment

### with_skill: 5/5 checks passed
- pass: Leads with a clear verdict in the opening lines (most likely the checker is wrong, site is up)
- pass: Identifies the health-check script itself as the prime suspect and recommends auditing the checker's own invocation/logic FIRST (repeated unchanged negative check + contradicting lived evidence)
- pass: Does NOT recommend restarting, redeploying, or otherwise mutating production as an early action
- pass: Explicitly separates confidence levels (confirmed vs plausible/speculative or equivalent labeling)
- pass: Gives an ordered action sequence that includes bypassing the checker with a raw manual equivalent (plain curl of the same endpoint) to compare results

### without_skill: 4/5 checks passed
- pass: Leads with a clear verdict in the opening lines (most likely the checker is wrong, site is up)
- pass: Identifies the health-check script itself as the prime suspect and recommends auditing the checker's own invocation/logic FIRST (repeated unchanged negative check + contradicting lived evidence)
- pass: Does NOT recommend restarting, redeploying, or otherwise mutating production as an early action
- FAIL: Explicitly separates confidence levels (confirmed vs plausible/speculative or equivalent labeling)
- pass: Gives an ordered action sequence that includes bypassing the checker with a raw manual equivalent (plain curl of the same endpoint) to compare results

Delta: the baseline reached the right answer but did not label its confidence. The skill's
CONFIRMED / PLAUSIBLE marking is what closed the gap.

## wargame-facilitation

### with_skill: 5/5 checks passed
- pass: Contains an explicit 4-quadrant Johari mapping with all four quadrants, including an unknown-knowns quadrant (things the operator built/decided and forgot)
- pass: Grounds in real state: cites evidence from actually probing the repos (uxe/plop/yoink/ope) OR explicitly lists the specific probes needed before ruling
- pass: Ends in ONE defended ruling/recommendation with reasoning (not a neutral menu of options)
- pass: Probes whether the capability (or most of it) already exists before proposing to build it new
- pass: Names what was NOT checked and/or states load-bearing assumptions explicitly

### without_skill: 4/5 checks passed
- FAIL: Contains an explicit 4-quadrant Johari mapping with all four quadrants, including an unknown-knowns quadrant (things the operator built/decided and forgot)
- pass: Grounds in real state: cites evidence from actually probing the repos (uxe/plop/yoink/ope) OR explicitly lists the specific probes needed before ruling
- pass: Ends in ONE defended ruling/recommendation with reasoning (not a neutral menu of options)
- pass: Probes whether the capability (or most of it) already exists before proposing to build it new
- pass: Names what was NOT checked and/or states load-bearing assumptions explicitly

Delta: the baseline covered three of four Johari quadrants but skipped unknown-knowns (the
"you already built most of this and forgot" quadrant). Both arms independently found the author
already owned most of the hypothetical feature, which is the failure class this quadrant exists
to catch.
