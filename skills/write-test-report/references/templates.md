# Report template

Used by [write-test-report](../../write-test-report/SKILL.md). Report formats follow [exploratory-testing-techniques](../../exploratory-testing-techniques/SKILL.md) (adapted with credit from Dan Ashby, https://github.com/danashby/Exploratory-Testing-Skill; RIMGEA by Cem Kaner, as credited there).

## report.md

Prose, except the header block and bug list. Drop or shorten what the manager doesn't need.

```markdown
# QA report: <project>, <YYYY-MM-DD>
Findings summary: <one line, plain words: what was observed and who it affects, within what was sampled>
Evidence: <evidence folder>/<project>/<YYYY-MM-DD>/
Independent: <yes or no> · Target actually tested: <live, preview address, or local with commit> (unreachable: name the blocker and affected scope)
I directed and watched the testing. I viewed the evidence. I wrote the report. (correct any that isn't true)
Helpers: <none, or each helper: its job, skill loaded, validated in its transcript yes/no>
Evidence reviewed: <the "Evidence reviewed" line from notes.md; if the review wasn't done or some evidence couldn't be reviewed, say so, and which areas it affects>

## Summary

| Product area | Status colour (information only, not acceptance) | How deeply tested (deep, quick look only, or not touched) | Bugs and blockers (incl. environment) |
|---|---|---|---|
| <feature or page> | <colour: one line why, for its users> | <depth> | BUG-01, BUG-03; <blocker> |

(Colour meanings: "Status colour" in write-test-report. Never a pass rate.)

## 1. The brief
What the charter asked for, what was in and out of scope, and the quality goals.

## 2. Tools used
Driver, evidence capture, recording, review (if used), target settings, anything else.

## 3. What I did
The story in time order, from notes.md. For each step: what I did, what I expected, what actually happened (exact text, timings, visual state, console/network errors if visible), what I tried next and why, and any hesitation or hunch. Inline evidence, e.g. "At 09:06 (video/rec-01.mp4 @ 04:20, shots/04-longname.png) …". Mark BUG-NN where each bug appears.

## 4. What I didn't do or couldn't do
What I needed and didn't have: <each readiness gap: what was missing, how that was proven, what I asked for and the answer, what it cost the session; or "nothing">.
Skipped, out of scope, blocked, tool limits, and why. For each blocker or tool limit, how it was proven (tried, checked, or asked whom). Risky probes: "<probe>: not run: approval declined" or "<probe>: not run: approval pending". Coverage against the charter: what was and wasn't covered.

## 5. What happened
Results per check (PASS, FAIL or UNKNOWN), then the bug list:

BUG-NN entries in the format from write-bug-report (title with trigger, failure and consequence; starting conditions; shortest steps; what happened vs what should happen; actor (who meets or causes it, by what real means, or "anyone who views or fetches it"); who it hurts and how badly; how often; evidence).

Recommendations, for the owner to decide: in the owner's priority scheme if they have one, otherwise in the order you recommend, with why (advisory; any causal hypothesis labelled as such, with its evidence and uncertainty).

## 6. What was interesting
Oddities, hunches, near-misses, surprises, and noticed-but-out-of-scope items, even if not judged bugs.

## 7. What we learned
About the product, the risks, and the testing itself. Suggested next charters.

Stopped because: <copied from notes.md; format in test-session references/stopping-heuristics.md, "Recording a stop">
Cleanup: <the "cleanup done" line from notes.md>

```
