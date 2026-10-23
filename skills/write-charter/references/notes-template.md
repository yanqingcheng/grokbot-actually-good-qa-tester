# Notes template

Used by [run-test-session](../../run-test-session/SKILL.md) step 1 and [write-bug-report](../../write-bug-report/SKILL.md). Copy into the session folder and fill in. Report formats follow [exploratory-testing-techniques](../../exploratory-testing-techniques/SKILL.md) (adapted with credit from Dan Ashby, https://github.com/danashby/Exploratory-Testing-Skill; MCOASTER by Michael D. Kelly, RIMGEA by Cem Kaner, as credited there).

## notes.md (running, timestamped)

Stamp each line from a real `date +%T` call (step 1 of [run-test-session](../../run-test-session/SKILL.md)).

```markdown
09:02:10 [clock] rec-01 started at 09:02:10 (video time 0:00 = 09:02:10)
09:02:40 [action] opened <url>; expected <x>; saw <exact text or state>; load felt ~3s
09:04:05 [odd] button label flickers on hover; unsure if bug. shots/03-flicker.png
09:06:30 [bug?] 10k-char name accepted, page layout breaks. shots/04-longname.png, rec-01 @ 04:20
09:07:00 [next] trying same input in profile edit, since bugs cluster

## Skill log

- <phase> · <skill opened> · <time>

## User actions in scope (coverage list)

- <action> @ <target setting>: tried 09:06 (to its end), result, evidence; or not tried: <reason: lower risk, past the deadline, blocked>

## Plan changes

- <time> switched from <breadth/depth/line of work> to <…> because <what you saw>

## Side effects of ordinary use

- <illustration: the visit counter goes up by one per page load>

## Bugs

BUG-01: <entry in the write-bug-report format, written once in full when found; later lines only add to it>

## Claims ledger

BUG-01 time 09:06:30: video-verified (rec-01 @ 04:20)
```
