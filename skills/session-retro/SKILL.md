---
name: session-retro
description: >-
  Use last, after a QA report has been delivered:
  write a short, honest retro.md on what got in the way and what to improve,
  and send the feedback parts to the manager and the skills' maintainer.
---

*Version: 2026-10-22.r17 (r17: context-driven review fixes (r17c draft: decisions under stated uncertainty, proportionate review, report and retro content required with flexible shape; r17b: reasoned stops told to the manager at once; success as useful information with sampling and gaps, risk-led breadth and depth, colours information only, adaptable report and variants; confirm and retro always done); skill names without the 'qa' prefix; no separate skill for checking fixes: a change is chartered like any other request ("Chartering a change" in write-charter); earlier: early finish explained)*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are; question the brief before touching the product). General rules for every phase: [test-session](../test-session/SKILL.md).

# Session retro

**When:** the report has been delivered ([write-test-report](../write-test-report/SKILL.md)). Every session ends with a self-review and a retro; it is always done. Its shape can flex with the session: for a short round a few lines, or a short debrief, may be enough. **Next:** wait for the next request (a change landing, such as a fix, is a new request).

Record the retro in the session's evidence folder (`retro.md`, or the agreed place); a brief recorded debrief counts. Keep it short and honest. The sections below are a default menu; use the ones with something to say. Describe what happened and its effect; **never blame people**.

## Sections

1. **Where the session fell short of success** (see [test-session](../test-session/SKILL.md)): which risks or user actions that mattered went unexplored (and, if you finished before the timebox, why the mission was covered and what risks remain), which claims lack evidence or rest on times written down later, where the report disagreed with itself, and what in the brief, the skills, the tools or your own choices let that happen.
2. **Readiness** ("Plan and get resources" in [test-session](../test-session/SKILL.md)): what did I need that I didn't have? Did I ask for it? If not, what stopped me?
3. **Issues during the session:** environment, access, tools and time: what got in the way and what it cost.
4. **Feedback for the manager:** the quality of the brief, the charter, how quickly answers and decisions came, and anything that would have helped.
5. **Feedback on the tools:** what worked, what was slow, flaky or missing.
6. **Feedback on the skills:** what was unclear, missing or wrong in these QA skills, with the skill name.
7. **What I'd do differently next time.**
8. **Carry into the next charter:** open risks, untested areas, follow-up questions.

## Send

The content is required, the shape can flex. Send the manager whatever applies of the shortfall, readiness, manager feedback and skills feedback; if setup named a skills maintainer, send them the shortfall and skills feedback. Include where the retro is recorded. Use the same channel as the report.
