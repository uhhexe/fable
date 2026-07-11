---
name: fable-review
description: Use when judging finished or claimed-finished work — the user says "fable review", "review of record", "is this actually done", "check this before I merge", a PR/build/paper claims completion, or output needs a verdict before it ships.
---

# Fable Review — the review-of-record

Produces a **verdict backed by evidence gathered this session** — never a vibe read of a diff or a summary of someone's claims. The standing doctrine: **claims are not state; only live probes are.**

**REQUIRED BACKGROUND:** fable-mode §5 (Verification) and §6 (Reasoning) — this skill is those sections pointed at someone else's work.

## Procedure

1. **Identify the load-bearing claims.** What does this work say is true ("tests pass", "handles X", "deployed")? List them — these are what you verify, not the prose around them.
2. **Probe each claim live.** Run the tests yourself. Hit the endpoint. Load the page. Re-grep the live file. Merged ≠ shipped ≠ running — verify the surface the claim is actually about.
3. **Place every claim on the claim ladder** and report the rung honestly: "should work" (reasoned) < "compiles/typechecks" < "tests pass" (show the run) < "verified end-to-end" (drove the flow, observed behavior). Never present a lower rung in a higher rung's language.
4. **Attack the survivors.** For findings that matter, try to refute your own conclusion: what evidence would prove this wrong, and did I look? Where stakes justify it, spawn an adversarial second pass with repo access, prompted to REFUTE, requiring file:line evidence to overturn.
5. **Mark confidence explicitly** on every finding: CONFIRMED (observed this session) / PLAUSIBLE (inferred) / SPECULATIVE (pattern-matched). Cut or label the decorative ones.
6. **Name what you didn't check.** Absence must never read as coverage. One line: "Not exercised: X, Y."

## Verdict format

```markdown
VERDICT: <SHIP / SHIP WITH FIXES / DO NOT SHIP> — <one sentence why>

Confirmed (probed this session):
- <claim> — <the probe + result>

Findings:
- [CONFIRMED|PLAUSIBLE] <finding> — <file:line / evidence> — <what to do>

Not exercised:
- <the angles this review did not run>

Next executable action: <one concrete step>
```

## Red flags

- A verdict written without running anything this session.
- "Tests pass" without the run's output in hand.
- Every finding marked CONFIRMED — you probably didn't calibrate.
- Red reported diplomatically. Red is red, with the output attached.
