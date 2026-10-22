# Actually Good QA Tester — Grok Bot skill pack

This repo is a **portable pack of exploratory QA tester skills** (each folder is a `SKILL.md` an agent can load). The tester agrees a charter, tests a web app (or skills, documents or a process; other kinds of product through a variant), reviews its own evidence, and reports with a story-style report, screenshots and a screen recording, ending with a short retro. It asks its manager before anything risky. It finds and reports; it never fixes code.

There are two ways to use it:

- **Hosted:** chat with the ready-made Actually Good QA Tester bot on Grok Bot ([Grok Bot](https://x.ai/) is a hosted agent product). Skills are already bundled there.
- **Local:** install the folders from this repo into Cursor or another agent that reads `SKILL.md`, then start with **qa-tester-getting-started**.

**Version: r16.1** (2026-10-22). This names the whole set of skills; each skill also carries its own version line.

> **Caveat:** these skills have not yet been fully reviewed end to end. Use them, but read them critically and report anything that looks wrong.

## Start here

### 1. Use the hosted Grok Bot

Open the Grok Bot template and chat with that bot. Its first conversation walks you through setup. You do not need to copy folders from this repo.

### 2. Install into Cursor or another local agent

1. Clone or download this repo.
2. Copy **every** folder inside `skills/` into your agent's skills directory (keep the folder names and each folder's `references/`).
3. Start a chat with that agent and ask it to run **qa-tester-getting-started** (or open `skills/qa-tester-getting-started/SKILL.md` and follow it). After setup, send it a test request.

Copy the whole `skills/` tree, not a subset. Skills link to each other with relative links to the sibling folder's `SKILL.md`, so they resolve as long as the folders sit together.

## What's different

- It questions the brief before touching the product (testing, not just checking).
- It uses Yanqing Cheng's broad bug definition: an inconsistency between the software and what is reasonably expected or desirable.
- It keeps a who-matters list per project, with agents counted as people who matter alongside humans, and every HIGH or CRITICAL bug names who it hurts.
- It plans and asks for what it needs before testing, instead of ploughing on without it.
- It says what it didn't test: a red/amber/green summary by product area, never pass counts.
- The timebox is an upper limit, not a target; it picks a named stopping heuristic and says why it stopped. Stopping is never a sign-off.
- It self-reviews the charter and the report, and ends every session with a retro.

## Skills (12), in the order a tester uses them

| Skill folder | When you'd reach for it |
|--------------|-------------------------|
| [`what-is-testing`](skills/what-is-testing/SKILL.md) | Read first: what testing (vs checking) and a bug are, in plain words. |
| [`qa-tester-getting-started`](skills/qa-tester-getting-started/SKILL.md) | **Default entry** — the first chat with a new owner: manager, default target, who matters, risky categories, report destination, evidence folder, timebox, recording setup. |
| [`qa-tester-test-session`](skills/qa-tester-test-session/SKILL.md) | The index: the tester's role, rules for every phase, the phase skills in order, and the stopping heuristics. |
| [`qa-write-charter`](skills/qa-write-charter/SKILL.md) | A request arrives: check the brief against who matters, plan and get resources, agree the charter with the manager. |
| [`qa-run-test-session`](skills/qa-run-test-session/SKILL.md) | Charter confirmed: notes, clock-stamped recording, narrow probes, evidence and timing rules, how a session ends. |
| [`write-bug-report`](skills/write-bug-report/SKILL.md) | The moment a bug is found: one BUG-NN entry, the severity scale, who it hurts. |
| [`qa-review-evidence`](skills/qa-review-evidence/SKILL.md) | After the session, before any verdict: skeptical review of all evidence, then cleanup. |
| [`qa-write-test-report`](skills/qa-write-test-report/SKILL.md) | After the review: report with a red/amber/green summary by product area and the session story. |
| [`qa-session-retro`](skills/qa-session-retro/SKILL.md) | Last, after the report (and every re-test): a short, honest retro. |
| [`qa-retest-fixes`](skills/qa-retest-fixes/SKILL.md) | Fixes land: re-test the old bugs and the golden path, report, retro. |
| [`qa-skill-variants`](skills/qa-skill-variants/SKILL.md) | Before a charter for a non-web product (API, CLI, mobile app, agent, data pipeline). |
| [`exploratory-testing-techniques`](skills/exploratory-testing-techniques/SKILL.md) | The toolbox used throughout: oracles, tours, attacks, data heuristics. |

## House rules (optional, any host)

A host may add its own house-rules skill for things specific to its setup (taking turns on a shared machine, where test accounts and secrets live, who to escalate to, and its own answers to the setup questions). The generic skills never depend on one, and none ships here. `skills/qa-tester-getting-started/references/grok-bot-box.md` is an optional platform reference for running on Grok Bot; ignore it on other hosts.

## Credits

- **James Bach and Michael Bolton**: ideas about testing (Rapid Software Testing, the context-driven school), and the [stopping heuristics](skills/qa-tester-test-session/references/stopping-heuristics.md) (Bolton's names, developed with Bach; with **Cem Kaner**'s Mission Rejected and **Joe Harter**'s split of Pause That Refreshes).
- **Yanqing Cheng**: definition of a bug, ["What even is a bug anyway?"](https://x.com/YanqingCheng/status/2092296333352652927).
- **Dan Ashby**: techniques adapted with credit from his [Exploratory Testing Skill](https://github.com/danashby/Exploratory-Testing-Skill), keeping every author credit he gives (including Cem Kaner's attacks and RIMGEA, and Michael D. Kelly's tours and MCOASTER). `skills/exploratory-testing-techniques/references/heuristics.md` is his text unchanged, with labelled pack notes, used under MIT — see [NOTICE.md](NOTICE.md).

## License

MIT — see [LICENSE](LICENSE). Copyright (c) 2026 Yanqing Cheng. Third-party notices are in [NOTICE.md](NOTICE.md).
