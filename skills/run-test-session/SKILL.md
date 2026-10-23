---
name: run-test-session
description: >-
  Use once the manager has confirmed the QA charter, while you are testing:
  session notes, a recording with a trustworthy clock, narrow probes,
  evidence and timing rules, reasoned stopping, and wind-down.
---

# Run the test session

You own this phase: "You own the testing" in [test-session](../test-session/SKILL.md).

You are here once the charter is confirmed (risky probes only once okayed). Next: at the first bug, open [write-bug-report](../write-bug-report/SKILL.md). When you stop, open [review-evidence](../review-evidence/SKILL.md). Rules for every phase: `test-session/references/session-rules.md`. Entering here directly? Open [test-session](../test-session/SKILL.md) first and complete its prerequisites.

## Progress reports

**Send the manager a short progress report at each moment you can recognise: after the smoke run, when you find a bug, when the plan or scope changes or you're blocked, and at the stop.** Three lines: what I did, what I saw, what's next. It gives the manager, and anyone watching, a chance to redirect early. Copy any observer named in the charter. Carry on with safe work unless told otherwise.

## Set up notes and recording

1. Keep session notes in `notes.md` (template: `write-charter/references/notes-template.md`). Write each line when it happens, stamped from a real `date +%T` call made then (or your script printing it). Log every action, expectation and observation (exact text, timings, visual state, console or network errors), every hunch and small weirdness. Don't pre-filter. Never estimate or reconstruct a time from memory or file dates. A line you missed gets the time you write it, marked `(late entry)`.
2. Record with a clock you can trust, using your setup's recording method (for a website, a screen recording with a clock burned in). Take any lease first ("Leases and locks" in `test-session/references/resource-cleanup.md`). Smoke-check that the capture starts and plays (`ffprobe`, and render one frame with `-frames:v 1` to see the overlay). Prefer several short clips to one long one. Commands on a Grok Bot box: `getting-started/references/grok-bot-box.md`, and `getting-started/references/grok-bot-box-sound.md` for sound or speech.
   - Every clip needs a way to map video time to clock time: a clock in the picture, or the clip's start time in `notes.md`.
   - Read reported times off the video clock. Without one, use your script log (tester-reported). Never use a subagent's estimate.
   - Headless: record the page itself and burn in its clock (on a Grok Bot box: "Recording a headless browser" in `getting-started/references/grok-bot-box.md`), and log each event's clock time from your script.
   - If recording fails, pause the work that depends on it and tell the manager. Switch only to a fallback agreed at readiness.
## Explore

Explore realistically ("You own the testing" in [test-session](../test-session/SKILL.md)). A helper driving the visible browser gets short steps and shows you each screen.

3. Choose where to start, and note where and why. An open look over the affected surfaces (each page, dialog, menu and widget, at the target settings) often shows problems early. Let the mission decide (for one fleeting timing bug, go straight to it).
4. Before each probe, check its input matches the actor ("Input must match the actor" in `test-session/references/actor-rules.md`). Keep a coverage list of user actions in `notes.md`, including what users can reasonably believe they can do. Something that invites an action and then does nothing is a finding (a "press start" prompt, an image styled as a button). Try each action to its end the way that user would, with input they could really give (the product's sign it is finished, or where the user would give up). Never take a shortcut such as loading a page by URL instead of clicking to it. Mark what you tried, with the result, and what you skipped, with why.
5. Drive with narrow probes, one focused goal per call ("enter a 10,000-character name in signup, submit, report the exact result and any console errors"). If you script it, the script log is the transcript. Never claim a test you didn't drive, or for a reading target, read yourself.
   - Never force a failed action. Record it and work out tool or product ("Tool or product?" in `test-session/references/actor-rules.md`).
   - Give the driver an allow-list of controls and keys, never a deny-list.
   - Controlled check: you give the exact values and buttons for every submission. If the page needs a choice you didn't give, the driver stops and reports.
   - Give a helper only the step and reference it needs now, never all the phase skills at once.
   - Submission guard: give each value with its on-screen context (`Field labelled Full name under Billing details: type Ada Lovelace`). Before submitting, the driver reads back the labels and submits only if they match. After submitting, it reports the response. A surprise that carries risk (a write that may have gone wrong, real data, money, messages) stops it. Other surprises are logged.
## Evidence and timing

6. Evidence and timing rules (apply as you go):
   - Capture each finding, odd state and successful state needed to support a status claim, when it happens.
   - **Every finding needs evidence that fits its claim and target, and a time.** Interactive target: a capture (screenshot, or console or network log for what a shot can't show). Reading target: source version, location, exact quotation and when you read it. A screenshot can't show timing or cause.
   - Save shots as `shots/NN-<slug>.png` and log each path. Prefer contact sheets to a small shot cap. Check each frame matches its label before you cite it.
   - Mark each finding observed, reproduced (with conditions), inferred or unverified. Say what evidence is missing. With none, write "seen once, no evidence". Never drop it.
   - Define every timed interval by its start and end events, as clock times ("request = Enter pressed, shown = card text renders"). Never report a bare duration.
   - Timing-window bugs: measure your driver's real gap between actions first. If too slow, pre-stage the second action (pre-type the URL in a spare tab, send close and Enter as one key sequence), then measure the gap on the video. Log each try's gap against the window as in or out (a stall past the window is out, with why). Keep every try. Revise the timing model if results challenge it.
   - Mis-clicks and setup accidents can produce the state under test: time and report them like any try.
   - Log every write (save, submit, answer, override): time, value (secrets by name), the app's response, whether you overrode it, and who chose it.
   - Link checks: each link is OK, broken or unknown. Broken only when the page is clearly gone or wrong (404, 410, a dead domain, a destination that isn't what the link promises). A block on automated checks (429, 403, 999, captcha) is unknown, with why. Give the three counts separately. Check an important unknown link once by hand. Don't retry fast past a block.
   - Claims ledger in `notes.md`: mark each time or fact in each finding video-verified, server-verified or tester-reported.
## Follow the charter's heuristics

7. Work the charter's heuristics, risk-based (stuck, or need a fresh angle: open [exploratory-testing-techniques](../exploratory-testing-techniques/SKILL.md) now), and follow hunches (bugs cluster). Move between breadth and depth (repeats of anything flaky, variants, double clicks, reload or Back mid-action, extremes). Note each switch and why. Attack as hard as the charter's risks call for on a safe target, choosing attacks by charter, risk and approvals, not all of them every time. Anything risky goes through the gate while you carry on with safe work.
## Recordings and video review

8. Stop each recording by its own pid (`kill -INT`). If the file keeps growing, find the pid writing it by its full path, check it is yours and stop it. If unsure, tell the manager. Wait until it exits, then decode it fully and read its length.
9. Optional: have a video-review helper (a watchVideo subagent) check clips for flicker, layout jumps, slow loads and error toasts. Add its findings to `notes.md`, marked as from video review.
## Stop

10. Stop on your reasoned judgement. Open `test-session/references/stopping-heuristics.md` before you decide to stop, and name the heuristic you used. Bolton: "we stop testing when we decide to stop testing".
    - The stop progress report (see "Progress reports") also gives the stopping reason, what was covered and the remaining risk. Record the stop in `notes.md` in the "Stopped because" format.
    - Prefer pausing to ask when a resource or scope change could unblock the mission, or when something material breaks mid-session: pause the affected work, ask, carry on with the rest, and resume once the revised mission can be met. A pause is not a stop. If stopping is better, stop.
    - Unagreed cost: **a cost to the owner that wasn't agreed at readiness is a reason to stop** that line and tell the manager. Agreed spend is fine (a paid API agreed for the core flow, but further exploring would start charging for a second service).
    - Mission rejected: if carrying on would harm someone, especially ethically, stop that work at once and tell the manager why. Continue unaffected work while they decide.
    - Blocked means nothing in scope can be tried after reasonable, cheap, permitted attempts (a headed browser, another recorder, your platform's recipes, asking). Record what you tried. Ask before changing the agreed setup.
    - Deadline (if the charter sets one): check `date` at each phase boundary and stop in time to report by it.
    - An early stop names each untried item with its reason.
    - Never stop because checks passed, "the main things work", "I've named what's left", or on an untested assumption. Untried items become follow-up work, with why.
## Wind down

11. Wind down: stop recordings and helpers you no longer need. You may keep the browser or dev server the evidence review needs. Full cleanup runs at the end of the evidence review.
