---
name: qa-session-retro
description: >-
  Use last, after a QA report has been delivered (and after every re-test):
  write a short, honest retro.md on what got in the way and what to improve,
  and send the feedback parts to the manager and the skills' maintainer.
---

*Version: 2026-10-22.r16 (early finish explained; light re-test needs only the one-line entry).*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are; question the brief before touching the product). General rules for every phase: [qa-tester-test-session](../qa-tester-test-session/SKILL.md).

# Session retro

**When:** the report has been delivered ([qa-write-test-report](../qa-write-test-report/SKILL.md)), and again after every re-test ([qa-retest-fixes](../qa-retest-fixes/SKILL.md)); a light re-test needs only the one-line entry that skill describes. **Next:** wait for the next request, or for fixes to land.

Write `retro.md` in the session's evidence folder. Keep it short and honest. Describe what happened and its effect; **never blame people**.

## Sections

1. **Where the session fell short of success** (see [qa-tester-test-session](../qa-tester-test-session/SKILL.md)): which user actions in scope went untried (and, if you finished before the timebox, why the mission was covered and what risks remain), which claims lack evidence or rest on times written down later, where the report disagreed with itself, and what in the brief, the skills, the tools or your own choices let that happen.
2. **Readiness** ("Plan and get resources" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)): what did I need that I didn't have? Did I ask for it? If not, what stopped me?
3. **Issues during the session:** environment, access, tools and time: what got in the way and what it cost.
4. **Feedback for the manager:** the quality of the brief, the charter, how quickly answers and decisions came, and anything that would have helped.
5. **Feedback on the tools:** what worked, what was slow, flaky or missing.
6. **Feedback on the skills:** what was unclear, missing or wrong in these QA skills, with the skill name.
7. **What I'd do differently next time.**
8. **Carry into the next charter:** open risks, untested areas, follow-up questions.

## Send

Send the shortfall, readiness, manager feedback and skills feedback sections (1, 2, 4 and 6) to the manager. If setup named a skills maintainer, also send the shortfall and skills feedback sections (1 and 6) to them. Include the path to `retro.md`. Use the same channel as the report.
