# Report template

Used by [qa-write-test-report](../../qa-write-test-report/SKILL.md). Report formats follow [exploratory-testing-techniques](../../exploratory-testing-techniques/SKILL.md) (adapted with credit from Dan Ashby, https://github.com/danashby/Exploratory-Testing-Skill; MCOASTER by Michael D. Kelly, RIMGEA by Cem Kaner, as credited there).

## report.md

Prose, not bullet fragments (the header block and bug index excepted).

```markdown
# QA report: <project> / <YYYY-MM-DD>
Evidence: <evidence folder>/<project>/<YYYY-MM-DD>/
Independent: yes/no · Target actually tested: <live / preview address / local + commit> (see qa-tester-test-session "Targets, accounts and independence"; unreachable target = red: blocked)
Evidence reviewed: <the "Evidence reviewed" line from notes.md; if the review wasn't done or some evidence couldn't be reviewed, say so: no area it covers can be green>

## Summary

| Product area | Judgement (red / amber / green) | How deeply tested (deep / quick look only / not touched) | Bugs and blockers (incl. environment) |
|---|---|---|---|
| <feature or page> | <colour: one line why, for its users> | <depth> | BUG-01, BUG-03; <blocker> |

(Judgement is a professional call, not a pass rate. Never "90% passed". Red = blocked or any CRITICAL; amber = HIGH/MEDIUM, or coverage incomplete: <untried user actions>; green = every in-scope user action tried with evidence, at most LOW bugs, and the evidence review complete for that area.)

> **MCOASTER** (what to summarise)
> Mission: <charter sentence> · Coverage: <areas explored> · Obstacles: <blockers> ·
> Audience: <manager; and who this session tested for> · Status: red / amber / green overall (one line why) ·
> Techniques: <heuristics used> · Environment: <target address, tools, target settings, build/commit if known> ·
> Risks: <found / confirmed / remaining>

## 1. The brief
What the charter asked for, what was in and out of scope, and the quality goals.

## 2. Tools used
Driver, evidence capture, recording, review (if used), target settings, anything else.

## 3. What I did
The story in time order, from notes.md. For each step: what I did, what I expected, what actually happened (exact text, timings, visual state, console/network errors if visible), what I tried next and why, and any hesitation or hunch. Inline evidence, e.g. "At 09:06 (video/rec-01.mp4 @ 04:20, shots/04-longname.png) …". Mark BUG-NN where each bug appears.

## 4. What I didn't do or couldn't do
What I needed and didn't have: <each readiness gap: what was missing, how that was proven, what I asked for and the answer, what it cost the session; or "nothing">.
Skipped, out of scope, blocked, tool limits, and why; for each blocker or tool limit, how it was proven (tried, checked, or asked whom). Risky probes: "<probe>: not run: approval declined" / "not run: approval pending". Coverage against the charter: what was and wasn't covered.

## 5. What happened
Results per check (PASS / FAIL / UNKNOWN), then the bug list:

BUG-NN entries in the format from write-bug-report (title with trigger, failure and consequence; starting conditions; shortest steps; what happened vs what should happen; actor (who meets or causes it, by what real means, or "anyone who views or fetches it"); who it hurts and how badly; how often; evidence).

Recommendations, for the owner to decide: in the owner's priority scheme if they have one, otherwise in the order you recommend, with why (advisory; no code fixes, no guesses at causes).

## 6. What was interesting
Oddities, hunches, near-misses, surprises, and noticed-but-out-of-scope items, even if not judged bugs.

## 7. What we learned
About the product, the risks, and the testing itself. Suggested next charters.

Stopped because: <stopping heuristic (see qa-tester-test-session references/stopping-heuristics.md), why it applied · Not covered: … · Risk remaining: … · Manager informed: …>
Cleanup: <the "cleanup done" line from notes.md>

**Verdict:** <one line, plain words: what happened and who it affects>
```
