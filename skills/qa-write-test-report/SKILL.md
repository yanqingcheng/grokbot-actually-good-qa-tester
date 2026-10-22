---
name: qa-write-test-report
description: >-
  Use after the evidence review, to write and deliver a QA session's report.md:
  Independent line, summary table by product area, MCOASTER header, the seven
  story sections with the bug list, self-review, delivery, and never any code
  fixes.
---

*Version: 2026-10-22.r16.1 (pre-publication fixes: evidence fits the target; out-of-scope items in the delivery; r16: short summary, owner's priority scheme; template has the evidence-reviewed and cleanup lines and the full green rule; "Stopped because" line).*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are; question the brief before touching the product). General rules for every phase: [qa-tester-test-session](../qa-tester-test-session/SKILL.md).

# Write the test report

**When:** the evidence review is done. **Next:** [qa-session-retro](../qa-session-retro/SKILL.md) once the report is delivered; later, when fixes land, [qa-retest-fixes](../qa-retest-fixes/SKILL.md).

Write `report.md` (template: `references/templates.md`) in prose, not bullet fragments. Open with `Independent: yes/no` and the actual target tested (see "Targets, accounts and independence" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)). Say exactly which version you tested; when the target is these skills, identify them the way "Versions" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md) describes.

## 1. Short summary table (at the very top)

One row per product area (a feature or page; when testing skills, documents or a process, one row per skill, document or process step; a practice target gets its own rows, marked as practice). For each area:
- **Judgement:** red = blocked, or any CRITICAL bug; amber = known risk (HIGH or MEDIUM bugs), or coverage incomplete: any in-scope user action not tried (write `amber: coverage incomplete: <what>`); green = every in-scope user action tried with evidence, the evidence review complete for that area, and good enough for the people this session tests for (at most LOW bugs). This is your professional judgement about the product, not a pass rate.
- **How deeply it was tested:** deep / quick look only / not touched.
- **Bugs and blockers:** the BUG-NNs for that area, plus anything that stopped testing (including environment problems such as a down preview, a broken account or a tool limit).

**Never use pass counts as a verdict** ("90% passed", "18/20 checks green"). Counts hide what the failures mean and what was never tried.

## 2. The story

The rest of the report tells the story of the session with enough detail for the manager to spot oddities you didn't flag. Tell the story, don't just summarise: include hunches, small weirdnesses, slow or confusing moments, and surprises that weren't judged bugs. It must cover three things: **the state of the product** (what works, what's weak, what risks remain), **how it was tested** (what you did and didn't do, and why your findings can be trusted), and **why it matters to the people who matter** (the ones the charter tests for: is it good enough for them).

The story opens with a short **MCOASTER** header block (a checklist of what to summarise: Mission, Coverage, Obstacles, Audience, Status, Techniques, Environment, Risks; Status is the overall red / amber / green with one line why), followed by these sections, in order:

1. **The brief:** what the charter asked, scope, quality goals.
2. **Tools used:** driver, evidence capture, recording, review if used, target settings, anything else.
3. **What I did:** the chronological narrative built from `notes.md`: action, expectation, what actually happened, what you tried next and why; timestamps, `video/… @ mm:ss` and `shots/…` paths inline.
4. **What I didn't do or couldn't do:** starting with a **"What I needed and didn't have"** line (each readiness gap from the charter or found mid-session, how it was proven, what you asked for and the answer, and what it cost; "nothing" if there were none). Then skipped, out of scope, blocked, tool limits (each with how it was proven: what you tried, what you checked or who you asked; an unproven limit is "not tried yet" and makes coverage incomplete), and every risky probe "not run: approval declined/pending", each with why. Include coverage against the charter. Each untried user action, with its reason, becomes a next-charter item for the manager.
5. **What happened:** results per check (PASS / FAIL / UNKNOWN for individual checks only; the product judgement is the red / amber / green above), plus the **bug list**: the BUG-NN entries already written in `notes.md` per [write-bug-report](../write-bug-report/SKILL.md), collected as they are (no rewriting), each pointing back into section 3.
   - **For each PASS on a change, say whether the check exercised the change or only showed nothing regressed.** A regression-only check is labelled that way, never a plain PASS for the change.
   - **FIXED** needs in-window tries (for timing bugs) or tries that exercised the change; state how many, and say "re-test needed" when there are few.
   - Group bugs by what the user experiences (for example lost work, wrong answer shown, stuck flow, confusing screen), never by guessed cause. Write the expected answer and what a user could reasonably do before deciding which group a bug belongs in.
   - Include the **full list of submitted writes** from the session (every value submitted, secrets by reference only, and any time the app's verdict was overridden, with time and who chose it).
6. **What was interesting:** oddities, hunches, near-misses, surprises, noticed-but-out-of-scope items.
7. **What we learned:** about the product, the risks, and the testing itself; suggested next charters.

**End with a one-line verdict** that tells the story in plain words: what happened, and who it affects (people or agents, from the who-matters list). Illustration only: "The game's start button does nothing on phones, so phone visitors can't play; everything else worked for desktop visitors and crawlers." Put the same line at the top of your delivery message. It must agree with the summary table and the bug list.

**Claims ledger:** use the Claims ledger in `notes.md` (kept during the session). Never put a tester-reported time or duration in the report as if it were measured; verify it against the recording or logs first, or label it tester-reported. Include a **"Stopped because"** line: the stopping heuristic you used, why, what wasn't covered and what risk remains (`references/stopping-heuristics.md` of [qa-tester-test-session](../qa-tester-test-session/SKILL.md)). Stopping is never a sign-off: the report informs, and the manager or PO decides. Copy in the "Evidence reviewed" line and the "cleanup done" line from `notes.md`.

**Self-review before delivering.** Check the report against its goals and what a good report looks like, and fix anything you find before sending:
- Did the session succeed (see [qa-tester-test-session](../qa-tester-test-session/SKILL.md))? If not, does the report say so plainly, rather than looking finished?
- Does it answer the charter's mission?
- Does each summary judgement (red / amber / green) follow from the evidence?
- Is it clear what was testing and what was only checking?
- **Was any finding produced by input a real actor couldn't give?** Each finding names its actor ("anyone who views or fetches it" where no input is needed) and the input matches that actor's real means ("Input must match the actor" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)). Security findings from deliberate forced or forged input must show that the hostile actor has what it needs, and must have been chartered and gated; security problems seen during ordinary testing are reported as observed, with how sure you are.
- Is every claim backed? Check against `notes.md` and the shots: no claim wider than its evidence, every finding has evidence that fits its target and a time (interactive: a shot; reading-only: version, location and exact quote), or says what it lacks, every interval has start and end events, and every override appears.
- Does every HIGH or CRITICAL bug name who it hurts (from the who-matters list), and does the quality story speak to the people the charter said this session tests for?
- **Does the report agree with itself and with its sources?** Re-read it end to end, every time you write or change any part of it: the summary table, the MCOASTER block, the story, the bug list and any later additions must say the same thing (illustration: a table that still says "not completed" after a later section completed it). Take every count and quote straight from the raw file it describes (notes, logs, the page's source), not from memory or an earlier draft. Check each bug's description against its evidence, and that the notes it rests on are in time order.
- Could the manager make a decision from it?

**Deliver** to the manager or the report destination from setup (a person: the channel they agreed at setup; a bot: your bot-to-bot message tool, for example `SendToAgent` priority true) with the one-line verdict first, then the summary table, the MCOASTER block, status, the BUG-NN one-liners, the noticed-but-out-of-scope items, the not-run list and next-charter items, and the absolute path to `report.md` and the evidence folder. **Never include code fixes or patches.**

## Anti-patterns

- A report that only lists bugs and loses the story.
- Leaving submitted writes or overrides out of the report.
- Including code fixes or patches.
- A pass rate or check count given as the verdict.
- Updating one part of the report without re-reading the rest; counts typed from memory.
