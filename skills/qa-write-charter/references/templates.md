# Session templates

Used by [qa-write-charter](../../qa-write-charter/SKILL.md) and [qa-run-test-session](../../qa-run-test-session/SKILL.md). Report template: [qa-write-test-report](../../qa-write-test-report/SKILL.md). Copy into the evidence folder and fill in. Report formats follow [exploratory-testing-techniques](../../exploratory-testing-techniques/SKILL.md) (adapted with credit from Dan Ashby, https://github.com/danashby/Exploratory-Testing-Skill; MCOASTER by Michael D. Kelly, RIMGEA by Cem Kaner, as credited there).

## charter.md

```markdown
# Charter: <project> / <YYYY-MM-DD>
- Project: <name, used for folder names>
- Manager: <who requested this; how to reach them>
- Target: <what and where (preview | live), with its version>
- Practice target (optional): <product used only to exercise the target; its bugs reported separately>
- Skills version: <bundle version, plus the most exact source you have; checked at confirm time>
- Access check: <reachable | reachable, browser check deferred (what's unchecked) | unreachable>, <time, how checked>
- Brief and setup questions raised: <each question, who you asked, the answer or "open">
- Mission: Explore <target>, with <resources/data/tools>, to discover <information about risks>.
- Who matters (project list, checked against this brief; mark guesses; confirmed by manager (or whoever house rules name): yes / pending): <users, payers, support/operators, data readers, people hurt if it breaks; human and agent alike>
- This session tests for: <which of those people, and what each would reasonably expect>
- Risks and actors: <each risk evaluated → its actor (person or agent, ordinary or hostile) → the means that actor really has (illustrations: touch, keyboard, screen reader, the API the product offers; for a named security risk, the forged request or tampering and the access it needs, gated)>
- Scope in: <flows, pages, features>
- Scope out: <explicitly not tested>
- Quality goals: <intent / acceptance notes, done-when>
- Heuristics: <oracles, e.g. FEW HICCUPPS Claims + User Expectations>; <tours>; <attacks>; <data heuristics>
- Target settings: <from setup defaults unless the charter says otherwise; for people (illustrations: screen size, browser, signed in or out, a person using a screen reader) and for agents (illustrations: no JavaScript, a crawler's or AI agent's user agent)>
- User actions in scope: <each action, or group of actions, and the target settings it is tried at; the user it is for>
- What exercises each change: <per change: the input or state that makes it run; or "no change: exploratory">
- Timebox: <sized to this mission and why; short rounds are normal for checks, re-tests and validation>
- Readiness (plan and get resources; see qa-tester-test-session):
  | Needed for the mission | State: proven / missing / unverified, with evidence (time, proof path, what was tried) | Material? | Asked for / charter narrowed |
  |---|---|---|---|
  | <tools, accounts, test data, devices and target settings, the actor's input means, permissions, time> | <illustrations: "proven: sound, 14:02, shots/level.txt -21 dB"; "proven: speech, browser lists 12 voices 5 s after load (shots/voices.txt)"; "unverified: speech, browser shows 0 voices, speech settings not yet checked; asked manager 14:05"> | <yes / no> | <whom, when, answer or "open"> |
- Pre-approved risky probes: <from the request, or "none">
- Risky probes requested (gate):
  | # | What | Where | Why | Worst case | Undo | Status (okayed / declined / pending) |
  |---|------|-------|-----|------------|------|------|
- Confirmed by manager: <yes / time>
```

## notes.md (running, timestamped)

Each line is written when it happens, with the time read off a clock then; reconstructed times start with `~` and say so.

```markdown
09:02:10 [clock] rec-01 started at 09:02:10 (video time 0:00 = 09:02:10)
09:02:40 [action] opened <url>; expected <x>; saw <exact text / state>; load felt ~3s
09:04:05 [odd] button label flickers on hover; unsure if bug. shots/03-flicker.png
09:06:30 [bug?] 10k-char name accepted, page layout breaks. shots/04-longname.png, rec-01 @ 04:20
09:07:00 [next] trying same input in profile edit, since bugs cluster

## User actions in scope (coverage list)

- <action> @ <target setting>: tried 09:06 (to its end), result, evidence / not tried: <reason>

## Side effects of ordinary use

- <for example: the visit counter goes up by one per page load>

## Bugs

BUG-01: <entry in the write-bug-report format, written once in full when found; later lines only add to it>

## Claims ledger

BUG-01 time 09:06:30: video-verified (rec-01 @ 04:20)
```
