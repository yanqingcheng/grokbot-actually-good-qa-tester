# Actually Good QA Tester

An exploratory QA tester for your agent, as a portable pack of skills. Each folder in `skills/` is a `SKILL.md` an agent can load.

Give it a web app to test (or skills, documents or a process; other kinds of product, such as an API, a command-line tool, a mobile app or an agent, through a variant). It agrees a charter with you, makes sure it has what it needs, tests like a real user would, checks its own evidence, and tells you what it found in a plain, story-style report with screenshots and a screen recording. It finds and reports problems; it never fixes code.

**Version: r19.**

## What makes it different

**It tests, not just checks.** Before it touches the product, it questions the brief: who matters here, what would they reasonably expect, and what could go wrong for them? Agents count as people who matter, with equal standing alongside humans. Risk steers where it goes broad and where it goes deep. Every session runs under a charter that its manager confirms, even if only with a one-line reply.

**It asks for what it needs.** Between drafting the charter and starting work there's a readiness step: plan and get resources. The tester lists what the mission needs, proves each item works or records it as missing, and asks for anything material, or for a narrower charter, instead of ploughing on without it. If it gets stuck mid-session, it prefers to pause and ask; if it decides to stop instead, it tells its manager straight away why, what was covered and what risk remains.

**Its input matches the real actor.** Every finding names who would hit it, and counts only if that person or agent could really do what the tester did, with the means they really have. Forcing clicks or injecting events doesn't count for an ordinary user. Security testing is the exception, and only when the charter names that risk and it's been approved.

**Its bugs come with evidence.** It uses Yanqing Cheng's broad definition of a bug: an inconsistency between the software and what is reasonably expected or desirable. Each bug is written once, in full, says who it hurts, and is backed by evidence that the tester reviews sceptically before giving any verdict.

**It knows when to stop, and doesn't sign off.** There's no time budget; a deadline is set only when you need results by a set time. The tester chooses from Bolton and Bach's stopping heuristics and says why it stopped in a "Stopped because" line. Stopping is never a sign-off: testers inform the people who decide whether to ship.

**Its reports tell the story.** A summary by product area says what was sampled and what wasn't tested, never pass counts; status colours, if used, are information only, never acceptance. Then comes the plain story of the session and the bug list, shaped to what the audience needs. Each session ends with a short, honest retro.

**It stays safe.** Risky probes need the manager's approval first. Some lines hold even with approval: it never uses the owner's real personal credentials or payment methods, and never messages real people outside the test.

**Where it deliberately goes beyond pure context-driven practice.** Agents count as people who matter, with equal standing (because agents increasingly use and depend on products), and every session has a quick charter confirm and a retro, even in variants (because a shared understanding up front and learning afterwards are worth their small cost). Context-driven testing would leave both to each context; here they are fixed on purpose.

## How a session flows

1. **Charter:** a request arrives; the tester drafts the charter with its manager.
2. **Readiness:** plan and get resources, raise any gaps, then the manager confirms.
3. **Session:** test with timestamped notes, a recording and real input, then review the evidence.
4. **Report:** deliver the report, with why it stopped and what's left.
5. **Retro:** a short look at what got in the way and what to improve.
6. **Changes:** when a change or fix lands, it is chartered like any other request (see "Chartering a change" in [write-charter](skills/write-charter/SKILL.md)).

## Getting started

### 1. Use the Grok Bot template

Create a bot from the Actually Good QA Tester template on [Grok Bot](https://x.ai/). On its first turn it runs [skills-setup](skills/skills-setup/SKILL.md): it downloads this repo, installs the skills in `skills/`, then sets up with you.

### 2. Install into Cursor or another agent

1. Clone or download this repo.
2. Copy **every** folder inside `skills/` into your agent's skills directory. Keep the folder names and each folder's `references/`.
3. Ask the agent to run **skills-setup** (or open [its SKILL.md](skills/skills-setup/SKILL.md) and follow it). It skips the install, since the skills are already there. It sets up a manager, a default target, who matters, report destination and the rest. Then send it a test request.

Copy the whole tree, not a subset: the skills link to each other with relative links, which resolve as long as the folders sit together.

## Skills, in the order a tester uses them

| Skill | When you'd reach for it |
|-------|-------------------------|
| [`what-is-testing`](skills/what-is-testing/SKILL.md) | Read first: what testing and a bug are, in plain words. |
| [`skills-setup`](skills/skills-setup/SKILL.md) | **Start here.** Installs the pack if needed, then the first chat with a new owner: gather and save the setup answers. |
| [`test-session`](skills/test-session/SKILL.md) | The index: the tester's role, rules for every phase, and the phase skills in order. |
| [`write-charter`](skills/write-charter/SKILL.md) | A request arrives (including a change or fix that has landed): question the brief, plan and get resources, agree the charter. |
| [`run-test-session`](skills/run-test-session/SKILL.md) | Charter confirmed: notes, recording, probes, evidence, and how a session ends. |
| [`write-bug-report`](skills/write-bug-report/SKILL.md) | The moment a bug is found: one full entry, its severity and who it hurts. |
| [`review-evidence`](skills/review-evidence/SKILL.md) | After the session, before any verdict: a sceptical review of all evidence, then cleanup. |
| [`write-test-report`](skills/write-test-report/SKILL.md) | Write and deliver the report. |
| [`session-retro`](skills/session-retro/SKILL.md) | Last, after the report is delivered: a short, honest retro. |
| [`skill-variants`](skills/skill-variants/SKILL.md) | Before chartering a product that isn't a website or web app. |
| [`exploratory-testing-techniques`](skills/exploratory-testing-techniques/SKILL.md) | The toolbox used throughout: oracles, tours, attacks, data heuristics. |

Useful references: [session rules](skills/test-session/references/session-rules.md), [stopping heuristics](skills/test-session/references/stopping-heuristics.md) and [heuristics](skills/exploratory-testing-techniques/references/heuristics.md).

## Optional extras

**House rules.** You can add your own house-rules skill for things specific to your setup: taking turns on a shared machine, where test accounts and secrets live, who to escalate to, and your own answers to the setup questions. The generic skills never depend on one, and none ships here.

**Grok Bot platform note.** [grok-bot-box.md](skills/skills-setup/references/grok-bot-box.md) is an optional reference for running on Grok Bot. Ignore it on other hosts.

## Credits

- **James Bach and Michael Bolton:** ideas about testing (Rapid Software Testing, the context-driven school) and the [stopping heuristics](skills/test-session/references/stopping-heuristics.md): Bolton's names, developed with Bach, with **Cem Kaner**'s Mission Rejected and **Joe Harter**'s split of Pause That Refreshes.
- **Dan Ashby:** techniques adapted from his [Exploratory Testing Skill](https://github.com/danashby/Exploratory-Testing-Skill), keeping every author credit he gives (including Cem Kaner's attacks and RIMGEA, and Michael D. Kelly's tours and MCOASTER). [heuristics.md](skills/exploratory-testing-techniques/references/heuristics.md) is his text unchanged, apart from labelled pack notes, used under the MIT License. See [NOTICE.md](NOTICE.md).
- **Yanqing Cheng:** the definition of a bug, ["What even is a bug anyway?"](https://x.com/YanqingCheng/status/2092296333352652927).

## License

MIT. See [LICENSE](LICENSE). Copyright (c) 2026 Yanqing Cheng. Third-party notices are in [NOTICE.md](NOTICE.md).
