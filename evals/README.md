# evals

An informal, small-sample benchmark of the `fable-mode` skill against a no-skill baseline. Published
so the "15/15 vs 13/15" figure in the README and SPEC is inspectable rather than asserted. Read the
limitations before quoting the number: it is the author's benchmark, not a proven result.

## What was measured

`fable-mode` is the umbrella skill (the operating character). The question was narrow: on a small set
of judgment-heavy prompts, does the skill change the output in the ways it claims to? It was not a
test of the five format skills, and not a test of whether the skill makes a weak model smart.

## Method

- **Scenarios:** three, in `evals.json`: war-game facilitation, orchestration planning, verification
  judgment. Each is graded against five pass/fail checks, so 15 checks in total.
- **Arms:** two. Baseline is the same model with no skill loaded; the other arm has `fable-mode`
  loaded. Nothing else differs.
- **Model:** Opus 4.8 ran both arms.
- **Grading:** automated by the skill-creator eval harness against each scenario's `checks`. An LLM
  graded the outputs; there was no human adjudication.
- **When:** a single run on 2026-07-07, the day the skill was built (iteration-1).
- **Results:** `iteration-1-results.md`, per-check.

## Result

15/15 with the skill, 13/15 without. The two checks the baseline missed:

1. **Verification scenario:** the baseline reached the right answer but did not label its confidence.
   The skill's CONFIRMED / PLAUSIBLE marking closed it.
2. **War-game scenario:** the baseline mapped three of four Johari quadrants and skipped
   unknown-knowns (the "you already built most of this and forgot" quadrant).

The orchestration scenario scored 5/5 in both arms. It did not discriminate.

## Limitations (read these before trusting the number)

- **The sample is tiny.** Three scenarios, one run, one model. This is a smoke test, not a study.
  Do not read "15/15" as an accuracy rate.
- **The baseline was already strong (13/15).** These runs used the author's own global config, which
  already encodes much of the operating character (tiers, papers, verification habits). The measured
  marginal lift is therefore narrow (two checks) and specific to that starting point. On a bare model
  with no such config the gap would probably be wider, but that was not tested here.
- **Grading was automated, single-grader.** An LLM judged pass/fail against the rubric. There was no
  human review of the grades and no inter-rater check. A stricter or a human grader could score
  differently.
- **The prompts are the author's real workload.** They name the author's own projects, so they are
  transparent but not neutral, generic benchmarks.
- **Raw outputs were not committed.** This publishes the spec and the graded verdicts, not the model
  transcripts that produced them, so the grades cannot be re-audited line by line from this directory.
- **The skill was edited after the run.** v1.3.0 gave every skill a human-voice pass, so the published
  `fable-mode` wording is not byte-identical to what was evaluated. The tested behaviors (Johari
  mapping, confidence labeling, papers, adversarial verification) are unchanged, but the eval was not
  re-run against the published text.

## Reproducing

The scenarios in `evals.json` are self-contained prompts. Run each against your model twice, once with
`fable-mode` loaded and once without, and grade the outputs against the `checks`. Your absolute scores
will differ from the author's: they depend on the model, the base config, and the grader. What the
scenarios test for is whether the skill produces explicit confidence marks, a full four-quadrant
Johari map, and papers-with-verification, versus a baseline that often reaches the same answer without
naming its confidence or its blind spots.
