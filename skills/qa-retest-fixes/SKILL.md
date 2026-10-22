---
name: qa-retest-fixes
description: >-
  Use when the manager says fixes have landed for bugs from an earlier QA
  session: re-test those BUG-NNs and the golden path in a new session, or do a light re-check for small or static fixes.
---

*Version: 2026-10-22.r16 (light re-test retro defined).*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are; question the brief before touching the product). General rules for every phase: [qa-tester-test-session](../qa-tester-test-session/SKILL.md).

# Re-test when fixes land

**When:** the manager says fixes landed for earlier BUG-NNs. **Next:** [qa-session-retro](../qa-session-retro/SKILL.md) after the re-test report.

**Results use one vocabulary:** **FIXED**, **PARTLY FIXED**, **NOT FIXED**, and **NEW** for a new problem found during the re-test (it gets the next unused BUG-NN).

## First, for every re-test

1. **Confirm the fix is in the version under test.** Note the version you are testing (build, commit, URL, or for skills the bundle version plus the most exact source you have, as "Versions" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md) says) and check the manager's claim that each fix is in it (for example the release note, the commit, or the changed wording). If a fix isn't there, report it as NOT FIXED (not in the version under test) and tell the manager before going further.
2. **Find the original entries.** Bug entries live wherever the original session kept them: the Bugs section of that session's `notes.md` by default, or wherever its report says.
3. **Choose the path** with the manager (one line is enough):
   - **Light re-test**, for small or static fixes (wording, docs, skills, config you can read): no full charter, and no new session folder unless the manager asks for one (if they do, name it by the same-day rule in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)). Re-read or re-check each fix against the original entry, then review in proportion: look at the changed material itself, compare it with the original finding and its evidence, and check that the result you record says only what you saw. In the report, name the kinds of evidence a full review would cover that don't apply here (for example no screenshots for a wording fix). This review stands in for [qa-review-evidence](../qa-review-evidence/SKILL.md) on the light path. Results go in the **original** session: under each bug's entry in its `notes.md` Bugs section (or wherever that session kept its bug entries), plus a one-line dated entry in its `retro.md`.
   - **Full re-test**, for anything that needs the product driven: the steps below.

## Full re-test

1. New dated session folder in your evidence folder (from setup), named by the same-day rule in [qa-tester-test-session](../qa-tester-test-session/SKILL.md) (`-2`, `-3` and so on if the date is taken).
2. Short charter ([qa-write-charter](../qa-write-charter/SKILL.md)) referencing the old BUG-NNs and the old session folder, confirmed with the manager as usual. For a timing bug, plan in-window tries; only those count toward FIXED.
3. Re-test those bugs and the golden path (the main flow a typical user takes when everything goes right), using [qa-run-test-session](../qa-run-test-session/SKILL.md), then [qa-review-evidence](../qa-review-evidence/SKILL.md).

## Recording results (both paths)

1. Add each result to the original BUG-NN entry (FIXED / PARTLY FIXED / NOT FIXED, with the version tested, the evidence and the folder). Full re-test: also note it in the new session's `notes.md`. Light re-test: the original entry is the only record, plus the one-line `retro.md` entry above; never rewrite the entry or open a duplicate. A new problem is NEW and gets the next unused BUG-NN ([write-bug-report](../write-bug-report/SKILL.md)).
2. Write the report again ([qa-write-test-report](../qa-write-test-report/SKILL.md)), including its self-review, with a re-test summary line counting FIXED, PARTLY FIXED, NOT FIXED and NEW. For a light re-test, this can be a re-test section added to the original report.
3. Retro ([qa-session-retro](../qa-session-retro/SKILL.md)), in proportion. Full re-test: the full retro in the new session folder. Light re-test: the one-line dated entry in the original session's `retro.md` (what was re-checked, the result, and any readiness, tool or skills feedback), sent with the re-test result; write the full sections only if something went wrong or you have feedback that needs them.
