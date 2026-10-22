---
name: write-bug-report
description: >-
  Use the moment you find a bug during a QA session: write its BUG-NN entry
  once, in full, so a developer understands it at once and the owner can
  decide whether to ship with it; afterwards only add to that same entry.
---

*Version: 2026-10-22.r17 (r17: context-driven review fixes (r17c draft: decisions under stated uncertainty, proportionate review, report and retro content required with flexible shape; r17b: reasoned stops told to the manager at once; success as useful information with sampling and gaps, risk-led breadth and depth, colours information only, adaptable report and variants; confirm and retro always done); skill names without the 'qa' prefix; no separate skill for checking fixes: a change is chartered like any other request ("Chartering a change" in write-charter); earlier: variations in proportion, not a count)*

> **Read [What is testing](../what-is-testing/SKILL.md) first** (what testing and a bug are). General rules: [test-session](../test-session/SKILL.md).

# Write a bug report

**When:** the moment you find a bug during [run-test-session](../run-test-session/SKILL.md). Write the entry **once, in full**, in the Bugs section of `notes.md` (see the notes template in [write-charter](../write-charter/SKILL.md)). Number it as described under "BUG-NN" in [test-session](../test-session/SKILL.md); this includes bugs that belong to another project, such as the skills or tools. Number bugs BUG-01, BUG-02, … across the whole project. Afterwards you only **add to that same entry** (new evidence, how far it reaches, answers to questions, later observations); never rewrite it from scratch. [write-test-report](../write-test-report/SKILL.md) just collects the entries into its bug list. A bug found during the evidence review is written the same way. **Next:** carry on testing.

## What a bug is

Something that makes the product worse for someone who matters. This is Yanqing Cheng's definition in plain words: an inconsistency between the software and what is reasonably expected or desirable (see [What is testing](../what-is-testing/SKILL.md)). UX confusion, broken expectations, spec gaps and process problems count, not only broken code.

## Your duty (bug advocacy)

"Bug advocacy" means making sure a bug gets understood and properly weighed, not just logged.
- Write it so a developer understands it at once and the owner can decide whether to ship with it.
- Follow up until it is understood: answer questions, add evidence, re-check if asked.
- **Observations first; hypotheses labelled.** Describe what happens and who it hurts. Investigating the cause (reading logs or source, narrowing conditions) is legitimate testing when it's useful and authorised; keep what you observed separate from what you suspect, label any causal hypothesis or suggested direction with its evidence and how sure you are, and never change the product's code yourself.

## Format

```
BUG-NN: <one sentence: what triggers it, what fails, and what that means for the user>
- Starting conditions: <account, data, target settings, address, build; for a skill, document or process bug: which one, its version, and the section or step>
- Steps (shortest that reproduce it): 1. … 2. … 3. …  (exact inputs; for a skill, document or process bug: the quoted wording, and what following it led to)
- What happened: <exact text / state>
- What should happen: <what a reasonable user, or the requirement, expects, and why>
- Actor: <who meets or causes it and by what real means (an ordinary visitor by keyboard, an agent by the requests the product offers, or for a security risk the hostile actor and the access it needs); "anyone who views or fetches it" when no input is needed; see "Input must match the actor" in [test-session](../test-session/SKILL.md)>
- Who it hurts and how badly: <in words: which people (human or agent) from the who-matters list, what they lose or risk, how often; then CRITICAL / HIGH / MEDIUM / LOW or "question: intended?">
- How often: <every time / N of M tries / seen once>
- Evidence: shots/NN-<slug>.png; video/rec-NN.mp4 @ mm:ss; notes @ HH:MM
```

Example title: "Saving a profile with a 300-character name wipes the whole form, so the user loses everything they typed."

## Rules

- Find the shortest steps: remove anything that isn't needed. To see how far it reaches (another place, another input, another target setting), try variations in proportion to the uncertainty, impact, safety and time left, and say what remains unknown.
- Every bug needs evidence that supports its claim, and a time ("Evidence and timing rules" in [run-test-session](../run-test-session/SKILL.md)): for an interactive target usually a capture; for a reading-only target the version, location and exact quotation. Say whether it is observed, reproduced, inferred or unverified, and what evidence is missing; with none, it is "seen once, no evidence".
- Severity is about the people harmed, not how hard it was to find. Say it in words first; the label comes second.
- **Every HIGH or CRITICAL bug names who it hurts**, using the people on the project's who-matters list (from setup and the charter). If it hurts someone not on the list, add them to the list and tell the manager. A bug matters because it bugs someone; if you can't say who, re-check the severity.
- **A default severity scale**, which the manager or house rules can replace with their own. Severity is a summary, not a substitute: say separately the impact, who is affected, how likely or how often, and how sure you are. Defaults:
  - **CRITICAL:** serious data loss, a serious security or money risk, a core flow blocked, or using up memory or other resources that the computer, or the people sharing it, need. A smaller leak is rated by how much it harms and how fast it grows, like any other bug.
  - **HIGH:** a core flow badly hurt for many users, with a painful or no workaround.
  - **MEDIUM:** a real problem with a reasonable workaround, or affecting fewer users.
  - **LOW:** minor or cosmetic.
  - **question: intended?** when it may be a design choice.
  Severity informs the report's status colours but doesn't set them ("Status colour" in [write-test-report](../write-test-report/SKILL.md)).
- One bug per entry. If unsure whether it is a bug or a design choice, report it with severity "question: intended?".
