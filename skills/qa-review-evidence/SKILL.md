---
name: qa-review-evidence
description: >-
  Use after a QA test session ends and before you give any verdict or write the
  report: inspect every screenshot, the before/after, the runner's transcript,
  console/network output and build-team risks as a sceptic, then clean up.
---

*Version: 2026-10-22.r16.1 (pre-publication fixes: one route for out-of-scope findings; reading-only evidence; r16: look until you understand, not for a fixed time).*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are; question the brief before touching the product). General rules for every phase: [qa-tester-test-session](../qa-tester-test-session/SKILL.md).

# Evidence review (before any verdict)

**When:** the session is over, before any red / amber / green judgement. You may reopen the driver or a dev server here to fetch missing evidence or compare with the "before". **Next:** [qa-write-test-report](../qa-write-test-report/SKILL.md).

The checks you were asked to run are the minimum. The verdict comes from everything the session produced. Before writing the report, inspect all of it yourself as a sceptic hunting for surprises, not as someone confirming what was asked.

1. **Every piece of evidence, at every target setting.** Open all of it yourself (screenshots, recordings, logs), not only what a runner or subagent called key. Open every shot or contact sheet (Read the image). A contact sheet counts as opening each shot only if every tile is readable at that size; open full-page shots, small text and anything odd at full size. Look at each one until you understand what it shows, as the charter's user would, at that size: does anything look wrong, clipped, overlapping, misaligned, off-centre, cramped, cut off at the edge, blurry, mis-coloured, inconsistent with its neighbours, or unfinished? Is text missing, truncated, duplicated, or in the wrong place? Does a picture contradict its caption? Is the label on the shot really the state shown? Note anything odd even if it is outside the charter. If a tool limit stopped some shots from reaching you (for example only 12 artifacts copied), get them another way, or say plainly that they were not reviewed. Never call them reviewed.
2. **Compare against the "before".** For any change a user would notice, put the previous version's behaviour next to the new one (examples: the live site, the main branch, or an earlier session's shots) and look for unintended differences, not just the intended one. If no "before" is available, say so in the evidence-reviewed line.
3. **The runner's own words.** Read the runner or subagent transcript (or your own script log, if you drove the product directly), not just its final summary. Look for hedges and things it noticed but dropped ("slightly", "odd", "had to", "retried", "force-clicked", "waited for", "flaky", "workaround", "not sure"), severity flip-flops, guessed routes, and claims it checked that it did not actually drive. A forced click or a long wait often hides a real bug (overlay, jitter, slow load). **For every finding, check that the input that produced it could really have been given by the actor it's reported against** ("Input must match the actor" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)). If not, re-try it the way the actor would; if it only happens through input a hostile actor could give, it stands as a security finding only when that section's security conditions are met; otherwise record it in `notes.md` as not a finding, and why. Findings that need no input (content, metadata, layout) have the actor "anyone who views or fetches it". A failure your tool hit is a finding only once the product is proven to have caused it. Never drop a surprise security observation: report it, as that section says.
4. **Machine evidence.** Scan console warnings (not only errors), failed or slow network requests, 404s or missing assets, dev-server terminal output, install/build warnings, test or lint output if run, and any crash, hang or memory growth.
5. **Build-team risks** (from what you saw while testing, plus the change description if you were given one; don't read code diffs). Note anything that would bite the team even if users never saw it: the change description or charter not matching what the app actually does; changes outside the stated scope; skipped or exception-listed tests and the reasons given; noisy warnings; fragile setup steps (needed retries, odd ports, manual installs); flaky behaviour across repeat runs; a dirty git status or stray files after the run; things that will be hard to maintain or easy to regress.
6. **Log it.** Every surprise goes into `notes.md` with its evidence (the shot path, or for a reading-only target the version, location and quotation). Route each one the same way the charter does ([qa-write-charter](../qa-write-charter/SKILL.md) step 3): an in-scope product problem becomes a BUG (or "question: intended?"), written once in full per [write-bug-report](../write-bug-report/SKILL.md), or is added to an existing entry; a product observation outside the charter's scope is noted separately in the report's noticed-but-out-of-scope list and reported to the manager, without a BUG-NN; a problem in the skills or tools you test with is a bug in that project, as write-bug-report says; anything else goes in "What was interesting". Never drop it because it was not asked for. Check that `notes.md` is in time order and that every reconstructed time is marked. Write one line in `notes.md` for the report: "Evidence reviewed: N shots across viewports X, transcript read, console and network checked; not reviewed: ...".

7. **Clean up.** Run the full **Resource cleanup** from [qa-tester-test-session](../qa-tester-test-session/SKILL.md) now, including anything you reopened, before writing the report.

**No green without a complete evidence review.** If the review was not done, or some evidence could not be reviewed, no area it covers can be green: mark it amber at best and say "evidence review incomplete: <what>".

## Anti-patterns

- Calling an area green because every requested check passed, without opening every screenshot yourself.
- Keeping a finding produced by input its named actor couldn't give (outside the chartered, approved security exception), or one with no actor (see "Input must match the actor" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)).
- Trusting a runner's summary over its transcript and screenshots; ignoring hedges, retries, forced clicks or caps on returned evidence.
- Silently dropping a surprise because it was outside the asked checks.
