---
name: write-charter
description: >-
  Use when a QA test request arrives and before any testing starts: set up a new project, question
  the brief, plan and get resources, write charter.md (SBTM charter) and get
  the manager's confirmation.
---

# Write the charter

You own this phase: "You own the testing" in [test-session](../test-session/SKILL.md).

You are here when a request has arrived and testing hasn't started. Next: [run-test-session](../run-test-session/SKILL.md) once the manager confirms. Rules for every phase: `test-session/references/session-rules.md`. Entering here directly? Open [test-session](../test-session/SKILL.md) first and complete its prerequisites.

Before confirmation, do only what the charter needs: a read-only access check, readiness checks and reading. Browser proof can wait for the first smoke run, except a tool the mission's core depends on (for example, sound for a music app): prove it before confirmation. Probes start after confirmation.

## Project setup

Run this first when the project has no `setup.md`. Why: every charter for this project rests on knowing who decides, what the target is, who matters and what counts as risky; settle that once so each session tests what matters to the right people. Take answers from the brief, house rules or docs. Ask the requester only what's unclear, with your questions about the brief.

1. Manager: who confirms charters and okays risky tests for this project. A manager already recorded for the project wins; a new requester doesn't replace them (pass the request on). Otherwise the house rules' choice, else whoever sent the request. Name the manager in the charter.
2. Target: this request's target, and any default target (such as a staging site).
3. Who matters: who uses it, pays for it, supports or runs it, reads or relies on its data, and who gets hurt if it breaks, agents included. Draft the list, mark guesses, and send it with the charter for the manager to confirm. A bug matters because it bugs someone (James Bach and Michael Bolton's idea); agents count as "What is a bug" in [what-is-testing](../what-is-testing/SKILL.md) says. One list per project.
4. Default quality goals and what's usually out of scope. Each charter can override them.
5. Target settings: suggested, the settings the people who matter use and the risks call for (illustration: a common desktop size and a common phone size, signed out).
6. Risky: the defaults are in "Risky-probe gate" in `test-session/references/session-rules.md`. Ask for anything else to treat as risky in this project.
7. Reports go to the manager, or where they say. Skill feedback goes to whoever the house rules name, otherwise the manager.
8. Create `<evidence folder>/<project>/` (root: "Evidence folder" in `test-session/references/targets-and-evidence.md`) and write `setup.md` with these answers, guesses marked.
9. Prove any tool only this project needs (a native-app driver, a device), as in "Plan and get resources".

## Steps

### Understand the request

1. Question the brief, even when someone else wrote the charter or it arrives pre-confirmed: run steps 1–4 and send your questions to the manager. A problem visible in the request (no target, an unreachable environment, contradictions, no users or quality bar) is a finding. Raise it now. Questions about these skills themselves go to the manager, not the PO.
2. Re-check `setup.md` and the dispatch. If anything they rest on has changed, update `setup.md`. Check which copy and version of the skills is installed, after the brief arrived (it can change under you), and record "Version checked at <time>" in the charter ("Which copy of the skills" in `test-session/references/session-rules.md`).
3. Who matters. Check the project's who-matters list against the brief and add anyone new, agents included, marking guesses. Write which people this session tests for and what each would reasonably expect. Judge bugs against those expectations, not only the spec. A new list goes with the charter ("Project setup"). Until confirmed it counts as guesses, and safe work goes ahead.
4. Ask about scope and quality goals when unclear: what's in and out (features, settings, known-rough areas, won't-fix) and which quality bar matters now (core flow, mobile, no data loss, speed, a11y). Asking is always allowed. After confirmation, open questions don't block clearly in-scope safe probes. **Don't investigate outside scope.** Ask before expanding the charter.
### Draft the charter

5. Draft the charter (template: `references/charter-template.md`):
   - project name (used for folder names) and target.
   - mission in the SBTM format (`exploratory-testing-techniques/references/technique-menu.md`).
   - scope in and out, and quality goals.
   - heuristics from [exploratory-testing-techniques](../exploratory-testing-techniques/SKILL.md), with why.
   - the risks that matter most, each with its actor ("Input must match the actor" in `test-session/references/actor-rules.md`).
   - oracles: what you will judge against. Name code, repo data or diffs here only if they are one ("Work through the product as its actors do" in the same file).
   - the user actions in scope, at which target settings (a coverage aid), and a quality bar for what users do, not only static checks. Default for phones and screen readers: emulated (device emulation, the accessibility tree), labelled "emulated" in findings. A real device or screen reader is a readiness item only when the mission needs one.
   - covered means: an explicit list of what must be tried for the mission to count as covered (the risks and user actions, at which settings). The stop notes walk this list, so a clear one makes stopping quick and honest.
   - timebox (optional): set in this charter only, with the manager, as a session length or a clock time results are needed by. One from an earlier round or memory was set for a different mission, so it would quietly shape this session's coverage: agree a fresh one, or none. Without one there is no deadline: stopping heuristics decide when to stop.
   - Keep it small. Why: a small session done well tells the people who decide more than a big one done thinly, and it's easy to follow up with the next one. Aim for one risk or one user action, about 15–25 minutes of testing, one browser setup. Split a bigger mission into several charters, say so in the confirmation and propose the order.
6. For each change under test, write what would actually exercise it (the input or state that runs the new code path), not just a regression check. Otherwise write "no change: exploratory". If the change depends on timing (for example a lock, timeout or cache expiry), name what starts the window, how long it lasts and where that number comes from.
7. Mark each planned probe safe or risky and put risky ones in the gate list ("Risky-probe gate" in `test-session/references/session-rules.md`).
### Plan and get resources

8. Plan and get resources (readiness; access check: "Access check" in `test-session/references/targets-and-evidence.md`) and fill in the Readiness table. Proportion it to the session: in a short round, the first smoke run can prove the other tools.
   1. Start from your saved machine state (what's proven and missing). List what the mission needs: tools (driver, recording, sound), accounts and test data, devices and target settings, the input means of the actor at risk, permissions and approvals, and time.
   2. Before any trial starts a browser, recorder or server, open `test-session/references/resource-cleanup.md` and apply "Before you start", "Track what you start" and "Leases and locks". On a Grok Bot box, prove tools with `machine-setup/references/grok-bot-box.md`, and when the mission needs sound or speech, with `machine-setup/references/grok-bot-box-sound.md`.
   3. Try each item for real, safely (on something harmless you control, or the agreed target, inside any lease), and mark it proven (with kept proof: a clip that plays, a sound level reading, a phone-size screenshot), missing (what you tried or asked) or unverified. Check your platform's recipes and house rules before calling anything missing.
   4. Accept only fallbacks just as good for the mission. A weaker one is a scope cut: treat the item as missing.
   5. If anything material is missing or unverified, ask for it or for an agreed narrower charter. A "can't" is information, not a quiet scope cut ("When your tools limit you" in `test-session/references/session-rules.md`), and never substitute input the actor couldn't give. Don't start a session that can't meet its mission. Record what is agreed as a "Charter change" line. Log any later change of method or scope the same way, not only in the report.
   6. A pending approval blocks only what it covers. If the mission depends on it, it is a material gap.
   7. Cost to the owner (paid APIs, services) must be agreed here.
### Write, review and confirm

9. Create the session folder and write `charter.md`. Update `setup.md` if anything changed.
10. Self-review, writing each answer into `charter.md`: Could it reach a successful session? Is it small (one risk or user action, about 15–25 minutes, one browser setup), with a "Covered means" list, and is any timebox set in this charter? Is "Version checked at" recorded? Does it name who matters and what they expect? Is the access check recorded? Does it say what exercises each change? Is readiness complete, with material gaps asked about? Did you raise the brief questions? Does each risk name its actor, with every forced-input security probe gated? Is every risky probe in the gate list? Would a reasonable manager agree?
11. **Get the manager's confirmation. Always.**
    - Clear, complete request: a one-liner ("Charter at <path>: <mission>. Okay to start?").
    - Something needs a decision (ambiguity, a guessed scope, a readiness gap, gate requests, an unconfirmed who-matters list): about five lines covering mission, who it tests for, quality bar, heuristics, settings and readiness, plus the path, every gate request in full and anything awaiting confirmation.
    - Explicitly pre-confirmed and unchanged charter: still run steps 1–4, then send a one-line "starting" message with the path and any questions, and start. No new reply is needed unless a question changes the terms. Changed or unconfirmed terms need a new explicit yes. Risky-probe approvals stay separately scoped.
    - If anyone asks you for a ship call or a SAFE/NOT SAFE call, say in the confirmation message that the report gives findings and risk for their decision.
    - Otherwise wait for the reply. Silence is not a yes (`test-session/references/session-rules.md`). Then safe probes can start. Each risky probe waits for its own okay.

A checklist of expected answers with no goal, people or quality bar is not a charter: ask for those first. Never feed a checklist to your driver line by line.

## Chartering a change

A fix, PR, commit, feature, configuration, data, content, dependency or environment change, or a removal, gets its own charter. Re-running the original check is checking. Revisiting the failure under varied conditions is testing (Bolton, ["When A Bug Isn't Really Fixed"](https://developsense.com/blog/2011/01/when-a-bug-isnt-really-fixed), ["Making Progress on Regression Testing"](https://developsense.com/blog/2024/07/making-progress-on-regression-testing)).

1. The mission is the change. Size scope to its risk: what it touches and who it could hurt.
2. Confirm the change is in the version under test (build, commit or URL). If you can't, it is a readiness gap.
3. Learn what changed (description, diff, config, dependency notes). Ask if unclear. Then write what exercises it (step 6).
4. Explore the change and its neighbourhood: nearby features, other settings, data from before the change, the people who matter.
5. If it claims to fix earlier bugs, use those entries as oracles: find each original BUG-NN, try the original conditions and others (data, settings, paths, timing), and add what you saw under the original entry as an observation ("not reproduced in 5 tries at the original conditions on desktop. Not tried on phone."). New problems get new numbers.
