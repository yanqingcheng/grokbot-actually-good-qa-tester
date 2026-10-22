---
name: qa-skill-variants
description: >-
  Use before a charter for a product that isn't a website or web app (an API, a
  command-line tool, a mobile app, an agent, a data pipeline): what
  never changes, what a variant usually changes, and how to make one with the
  manager's confirmation.
---

*Version: 2026-10-22.r16 (reading-only targets need no variant).*

> **Read [What is testing](../what-is-testing/SKILL.md) first.** General rules for every phase: [qa-tester-test-session](../qa-tester-test-session/SKILL.md).

# QA skill variants (non-web products)

**When:** before a charter for a product that isn't a website or web app, for example an API, a command-line tool, a mobile app, an agent or a data pipeline. Targets you test by reading (skills, documents, a process) need no variant. The core skills give web examples; a variant swaps them for ones that fit.

## Never changes

The success definition, the bug definition, who matters (people and agents, equal in standing), questioning the brief, the risky-probe gate and hard lines, the evidence rules, anti-jobs (the things a tester never does, such as fixing the code or deciding what the product is meant to do), self-review and the retro. A variant changes how you apply them, never what they mean.

## Usually changes

1. **Driver:** what operates the product (for example a shell, an HTTP client, a device emulator, the agent's own chat).
2. **Target settings:** the conditions that change what users experience (for example OS and locale, API version and role, device and OS version, input data shape).
3. **Evidence and recording:** a capture with a clock you can trust (for example a timestamped terminal transcript, logged requests and responses).
4. **Access check:** the first thing a user would do (for example run the version command, call the base address).
5. **User actions:** what users can do or reasonably believe they can do (for example every flag the help lists, every endpoint and parameter the docs mention, every link a response returns).
6. **Safe versus risky:** which ordinary actions write real data (for example a POST to a live API is a write; a command run in a scratch folder you made is safe).
7. **Who-matters prompts:** who uses it, including agents (for example scripts that parse the output, client apps, downstream jobs).

## How to make one

1. Copy the core skills you need to `<name>-<kind>` (for example `qa-run-test-session-cli`).
2. Edit only the parts above; leave everything else word for word.
3. Give the copy its own version line naming the core version it came from and what changed.
4. Send the manager a one-line summary of the changes and wait for them to confirm before the charter. Silence is not a yes.
5. In the retro, say whether the variant worked, so it can be improved.

## Worked examples (from a dry run on an API and a command-line tool)

- "Access check from a fresh signed-out profile" didn't fit: it became "run the version command with no credentials set" and "call the base address".
- "Every finding needs a screenshot": the capture became the exact command and output, or the full request and response.
- Screen recording didn't fit: a timestamped terminal transcript or request log replaced it.
- The smoke-run "browser opens" became "the tool runs its version command".
- "Look at every screen": every command's help and output, every endpoint's responses.
- "Is a command that writes local files risky?": safe in a scratch folder you created; any write to a live API goes through the gate.
- Evidence review "every screenshot, any visual change": every capture, and any change in output a user or script would notice.

