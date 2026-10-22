---
name: exploratory-testing-techniques
description: >-
  Use when planning, running, or reporting an exploratory test session and you
  need heuristics (rules of thumb), oracles, tours, attacks or data heuristics to
  pick a charter's lenses and argue why something is a bug.
---

*Version: 2026-10-22.r17 (r17: context-driven review fixes (r17c draft: decisions under stated uncertainty, proportionate review, report and retro content required with flexible shape; r17b: reasoned stops told to the manager at once; success as useful information with sampling and gaps, risk-led breadth and depth, colours information only, adaptable report and variants; confirm and retro always done); skill names without the 'qa' prefix; no separate skill for checking fixes: a change is chartered like any other request ("Chartering a change" in write-charter); earlier: pre-publication fixes: Ashby MIT copyright and permission notice; Ashby's text unchanged, with labelled pack notes; upstream pinned; r16: no durations in the pack's own text; pack note on Ashby's numbers (32-bit integer probes described))*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are; question the brief before touching the product).

# Exploratory testing techniques

> **Credit:** Adapted with credit from **Dan Ashby**'s *Exploratory Testing Skill*, https://github.com/danashby/Exploratory-Testing-Skill (original README states MIT; the copyright and permission notice is in `references/heuristics.md`, which marks Ashby's text and this pack's labelled notes). Heuristic authors are credited as Ashby credits them: FEW HICCUPPS (Michael Bolton & James Bach), SFDIPOT and CRUSSPIC STMPL (James Bach), FCC CUTS VIDS tours and MCOASTER (Michael D. Kelly), testing attacks and RIMGEA (Cem Kaner), data heuristics from the Test Heuristics Cheat Sheet (Elisabeth Hendrickson, James Lyndsay, Dale Emery), SBTM (James & Jon Bach). Full list and authors: `references/heuristics.md`.

Testing is how you learn about a product and look for the problems that matter; trying hard to make it fail is one of the best ways to find them. This skill is the menu of techniques. The step-by-step procedure for a session is indexed in [test-session](../test-session/SKILL.md) (charter, session, evidence review, report, retro, each its own skill; a change is chartered like any other request). The tester finds and reports problems and never fixes code.

## When to use

- Writing a charter: choosing which lenses to point at a target.
- Mid-session: stuck, or need a fresh angle ("what haven't I varied?").
- Arguing why an observation is a bug (name the oracle).
- Writing the session report (naming the oracle behind each bug).

## Charter format (SBTM, James & Jon Bach)

> **"Explore [target], with [resources/data/tools], to discover [information about risks]"**

Size each charter to its mission: small enough to stay focused, and only as long as it needs; checks, small changes and validation are often short. Durations in the adapted heuristics are Ashby's SBTM examples, not rules of this pack (see the note at the top of `references/heuristics.md`). Heuristics are a menu of lenses, not a checklist: select what is relevant and combine freely.

Plain-words glossary: a **heuristic** is a fallible rule of thumb; an **oracle** is a way to recognise a problem (something you compare the product against, such as a claim, a comparable product or a user's expectation); a **tour** is a themed route through the app; an **attack** is input or a sequence chosen to make it fail; **SBTM** is session-based test management (timeboxed sessions, each with a charter and a report).

## Pick heuristics for a charter

Choose the techniques that will find the problems that matter for this target and its risks, and say in the charter why you chose them. The table is a menu to think with (illustration: one or two from each row that applies is a good starting habit), not a quota. All are in `references/heuristics.md`.

| Need | Reach for |
|---|---|
| Recognise a problem (oracles) | FEW HICCUPPS: keep in mind throughout; in each bug, say plainly what the product is inconsistent with (illustration: its own claims, or a user's expectation) |
| Decide what to cover | SFDIPOT (product areas); CRUSSPIC STMPL (quality attributes); RCRCRC (after a change); W5HE / MIDTESTD (before starting) |
| Move through the app | FCC CUTS VIDS tours: Feature, Complexity, Claims, Configuration, User, Testability, Scenario, Variability, Interoperability, Data, Structure |
| Break it | Kaner attacks: Long Name, Special Characters, Boundary Value, Invalid Type, Null/Empty, Overload, Interruption, Sequence; plus the Part 5 data-type attack cheat sheet (string, numeric, date/time, file/path) |
| Choose values | Goldilocks, ZOM, CRUD (+ Dependencies), BME, Boundaries, Some/None/All, Sequences, Count, Sorting, Input Method Variations, Configurations, State Analysis, Map Making |
| Stress / resilience | Multi-User/Concurrency, Interruptions, Starvation, Flood; FIBLOTS/IVECTRAS for performance |
| Errors seen | FAILURE (Ben Simo) to judge the error handling itself |
| Mobile | I SLICED UP FUN |
| Prioritise order | SLIME, DUFFSSCRA (prompts to consider, not an ordering mandate: see the pack note by SLIME); "Bugs Cluster": found one, dig nearby |
| Quick sweeps | Part 13 rapid questions: security, performance, accessibility, i18n, concurrency & state |

Attacks are available tools, not an obligation: choose the ones the charter's risks call for. Any that are risky need the manager's okay first (see [test-session](../test-session/SKILL.md)).

## Report formats

[write-test-report](../write-test-report/SKILL.md) sets out the report structure (summary table, MCOASTER, the story sections, delivery), and [write-bug-report](../write-bug-report/SKILL.md) sets out bug entries. Produce the report automatically when the session ends; don't wait to be asked. Use the techniques here to choose lenses and to say plainly why each finding is a problem.

Fill-in templates: charter and notes in `references/templates.md` of [write-charter](../write-charter/SKILL.md); report in `references/templates.md` of [write-test-report](../write-test-report/SKILL.md).

Write bugs with RIMGEA (Cem Kaner): Replicate, Isolate, Maximise (show the real worst-case impact honestly, never exaggerate), Generalise, Externally describe, And report.

## Reference

- `references/heuristics.md`: every oracle, coverage model, tour, attack, data heuristic, data-type attack value, regression/error/reporting heuristic, wisdom rule, SBTM, rapid questions, and the mnemonic index, with authors.
