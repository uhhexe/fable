---
name: fable-exe-review
description: Use when judging finished or claimed-finished work: the user says "fable.exe review", "fable exe review", "review of record", "is this actually done", "check this before I merge", or a PR, build, or paper needs a verdict before it ships.
---

# fable.exe review: the review-of-record

Produces a **verdict backed by evidence gathered this session**, never a vibe read of a diff or a summary of someone's claims. The standing doctrine: **claims are not state; only live probes are.**

**Background:** fable-exe-mode §5 (Verification) and §6 (Reasoning). This skill is those sections pointed at someone else's work. The load-bearing rules are inlined below, so this file stands alone.

## Procedure

1. **Pin the target.** Fix exactly what is under review (the working-tree diff, a branch diff, a PR, a returned paper, a deployed surface) so every probe hits the surface the claims are about, not the version in your head.
2. **Identify the load-bearing claims.** What does this work say is true ("tests pass", "handles X", "deployed")? List them. These are what you verify, not the prose around them.
3. **Probe each claim live.** Run the tests yourself. Hit the endpoint. Load the page. Re-grep the live file. Merged ≠ shipped ≠ running, so verify the surface the claim is actually about. If a load-bearing claim cannot be probed from this environment, say exactly which probe is missing and why it cannot run here; that claim rides no higher than PLAUSIBLE, and the verdict is capped: unprobed load-bearing claims cannot back a clean SHIP.
4. **Place every claim on the claim ladder** and report the rung honestly: "should work" (reasoned) < "compiles/typechecks" < "tests pass" (show the run) < "verified end-to-end" (drove the flow, observed behavior). Never present a lower rung in a higher rung's language.
5. **Attack the survivors.** For findings that matter, try to refute your own conclusion: what evidence would prove this wrong, and did I look? Where stakes justify it (a finding that would flip the verdict or block a merge), spawn an adversarial second pass with repo access, prompted to REFUTE with file:line evidence and to say explicitly when it finds nothing (naming what it inspected). Its findings are claims too: verify them before they enter the verdict.
6. **Mark confidence explicitly** on every finding: CONFIRMED (observed this session) / PLAUSIBLE (inferred) / SPECULATIVE (pattern-matched). Cut or label the decorative ones.
7. **Name what you didn't check.** Absence must never read as coverage. One line: "Not exercised: X, Y."

## Verdict format

```markdown
VERDICT: <SHIP / SHIP WITH FIXES / DO NOT SHIP>. <one sentence why>

Confirmed (probed this session):
- <claim>: <the probe + result>

Findings:
- [CONFIRMED|PLAUSIBLE] <finding>: <file:line / evidence>. <what to do>

Not exercised:
- <the angles this review did not run>

Next executable action: <one concrete step>
```

**Land the verdict.** Post it where the next session finds it: a PR comment when reviewing a PR, otherwise a file on disk (the repo's existing convention, or `docs/reviews/YYYY-MM-DD-<target>.md`). A chat-only verdict rots. Papers over conversations.

## Red flags

- A verdict written without running anything this session.
- "Tests pass" without the run's output in hand.
- Every finding marked CONFIRMED: you probably didn't calibrate.
- Red reported diplomatically. Red is red, with the output attached.
- The verdict lives only in chat. Land it.
