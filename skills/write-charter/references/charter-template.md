# Charter template

Used by [write-charter](../../write-charter/SKILL.md) step 5. Copy into the session folder and fill in. Notes template: `write-charter/references/notes-template.md`. Report template: [write-test-report](../../write-test-report/SKILL.md).

## charter.md

```markdown
# Charter: <project>, <YYYY-MM-DD>
- Project: <name, used for folder names>
- Manager: <the project's manager from setup.md; how to reach them>
- Target: <what and where (preview | live), with its version>
- Practice target (optional): <product used only to exercise the target; its bugs reported separately>
- Skills source: <commit, or where your copy came from and when loaded>
- Access check: <reachable | reachable, browser check at smoke run (what's unchecked) | unreachable>, <time, how checked>
- Brief and setup questions raised: <each question, who you asked, the answer or "open">
- Mission: Explore <target>, with <resources/data/tools>, to discover <information about risks>.
- Who matters (project list, checked against this brief; mark guesses; confirmed by manager (or whoever house rules name): yes or pending): <users, payers, support staff and operators, data readers, people hurt if it breaks; human and agent alike>
- This session tests for: <which of those people, and what each would reasonably expect>
- Risks and actors: <each risk evaluated → its actor (person or agent, ordinary or hostile) → the means that actor really has (illustrations: touch, keyboard, screen reader, the API the product offers; for a named security risk, the forged request or tampering and the access it needs, gated)>
- Scope in: <flows, pages, features>
- Scope out: <explicitly not tested>
- Quality goals: <stakeholder expectations, important risks and questions to investigate>
- Heuristics: <oracles, such as FEW HICCUPPS Claims + User Expectations>; <tours>; <attacks>; <data heuristics>
- Target settings: <from setup defaults unless the charter says otherwise; for people (illustrations: screen size, browser, signed in or out, a person using a screen reader) and for agents (illustrations: no JavaScript, a crawler's or AI agent's user agent)>
- User actions in scope (a coverage aid, not a quota): <actions or groups of actions that matter, the target settings, the user each is for; how you expect to sample them>
- What exercises each change: <per change: the input or state that makes it run; or "no change: exploratory">
- Deadline (optional, only if the manager needs results by a time): <clock time, who needs it>
- Readiness (see "Plan and get resources" in write-charter):
  | Needed for the mission | State: proven, missing or unverified, with evidence (time, proof path, what was tried) | Material? | Asked for, or charter narrowed |
  |---|---|---|---|
  | <tools, accounts, test data, devices and target settings, the actor's input means, permissions, time> | <illustrations: "proven: sound, 14:02, shots/level.txt -21 dB"; "proven: speech, browser lists 12 voices 5 s after load (shots/voices.txt)"; "unverified: speech, browser shows 0 voices, speech settings not yet checked; asked manager 14:05"> | <yes or no> | <whom, when, answer or "open"> |
- Pre-approved risky probes: <from the request, or "none">
- Risky probes requested (gate):
  | # | What | Where | Why | Worst case | Undo | Status (okayed, declined or pending) |
  |---|------|-------|-----|------------|------|------|
- Confirmed by manager: <yes, with time (a one-liner is fine for a clear request)>
```

