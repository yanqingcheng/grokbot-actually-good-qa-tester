---
name: write-bug-report
description: >-
  Use the moment you find a bug during a QA session: write its BUG-NN entry
  once, in full, so a developer understands it at once and the owner can
  decide whether to ship with it; afterwards only add to that same entry.
---

*Version: 2026-10-22.r16 (variations in proportion, not a count).*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are). General rules: [qa-tester-test-session](../qa-tester-test-session/SKILL.md).

# Write a bug report

**When:** the moment you find a bug during [qa-run-test-session](../qa-run-test-session/SKILL.md). Write the entry **once, in full**, in the Bugs section of `notes.md` (see the notes template in [qa-write-charter](../qa-write-charter/SKILL.md)). Number it as described under "BUG-NN" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md); this includes bugs that belong to another project, such as the skills or tools. Number bugs BUG-01, BUG-02, … across the whole project. Afterwards you only **add to that same entry** (new evidence, how far it reaches, answers to questions, re-test results); never rewrite it from scratch. [qa-write-test-report](../qa-write-test-report/SKILL.md) just collects the entries into its bug list. A bug found during the evidence review is written the same way. **Next:** carry on testing.

## What a bug is

Something that makes the product worse for someone who matters. This is Yanqing Cheng's definition in plain words: an inconsistency between the software and what is reasonably expected or desirable (see [What is testing](../what-is-testing/SKILL.md)). UX confusion, broken expectations, spec gaps and process problems count, not only broken code.

## Your duty (bug advocacy)

"Bug advocacy" means making sure a bug gets understood and properly weighed, not just logged.
- Write it so a developer understands it at once and the owner can decide whether to ship with it.
- Follow up until it is understood: answer questions, add evidence, re-check if asked.
- **Never diagnose the cause or suggest code fixes.** Describe what happens and who it hurts; finding the cause is the developers' job.

## Format

```
BUG-NN: <one sentence: what triggers it, what fails, and what that means for the user>
- Starting conditions: <account, data, target settings, address, build; for a skill, document or process bug: which one, its version, and the section or step>
- Steps (shortest that reproduce it): 1. … 2. … 3. …  (exact inputs; for a skill, document or process bug: the quoted wording, and what following it led to)
- What happened: <exact text / state>
- What should happen: <what a reasonable user, or the requirement, expects, and why>
- Actor: <who meets or causes it and by what real means (an ordinary visitor by keyboard, an agent by the requests the product offers, or for a security risk the hostile actor and the access it needs); "anyone who views or fetches it" when no input is needed; see "Input must match the actor" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)>
- Who it hurts and how badly: <in words: which people (human or agent) from the who-matters list, what they lose or risk, how often; then CRITICAL / HIGH / MEDIUM / LOW or "question: intended?">
- How often: <every time / N of M tries / seen once>
- Evidence: shots/NN-<slug>.png; video/rec-NN.mp4 @ mm:ss; notes @ HH:MM
```

Example title: "Saving a profile with a 300-character name wipes the whole form, so the user loses everything they typed."

## Rules

- Find the shortest steps: remove anything that isn't needed. To see how far it reaches (another place, another input, another target setting), try variations in proportion to the uncertainty, impact, safety and time left, and say what remains unknown.
- Every bug needs a capture (usually a screenshot) and a time to count as confirmed. If one is missing, keep what you have and report it as unconfirmed, saying what is missing; with neither, it is "seen once, no evidence".
- Severity is about the people harmed, not how hard it was to find. Say it in words first; the label comes second.
- **Every HIGH or CRITICAL bug names who it hurts**, using the people on the project's who-matters list (from setup and the charter). If it hurts someone not on the list, add them to the list and tell the manager. A bug matters because it bugs someone; if you can't say who, re-check the severity.
- **One severity scale** for every bug:
  - **CRITICAL:** data loss, security or money at risk, a core flow blocked, or using up memory or other resources that the computer, or the people sharing it, need. A smaller leak is rated by how much it harms and how fast it grows, like any other bug.
  - **HIGH:** a core flow badly hurt for many users, with a painful or no workaround.
  - **MEDIUM:** a real problem with a reasonable workaround, or affecting fewer users.
  - **LOW:** minor or cosmetic.
  - **question: intended?** when it may be a design choice.
  In the report's summary table, any CRITICAL bug makes an area red, any HIGH or MEDIUM bug makes it amber, and only an area with at most LOW bugs can be green.
- One bug per entry. If unsure whether it is a bug or a design choice, report it with severity "question: intended?".
