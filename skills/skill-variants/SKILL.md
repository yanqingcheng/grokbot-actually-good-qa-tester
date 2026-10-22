---
name: skill-variants
description: >-
  Use before a charter for a product that isn't a website or web app (an API, a
  command-line tool, a mobile app, an agent, a data pipeline): what
  never changes, what a variant can adapt, and how to make one with the
  manager's confirmation.
---

*Version: 2026-10-22.r17 (r17: context-driven review fixes (r17c draft: decisions under stated uncertainty, proportionate review, report and retro content required with flexible shape; r17b: reasoned stops told to the manager at once; success as useful information with sampling and gaps, risk-led breadth and depth, colours information only, adaptable report and variants; confirm and retro always done); skill names without the 'qa' prefix; no separate skill for checking fixes: a change is chartered like any other request ("Chartering a change" in write-charter); earlier: reading-only targets need no variant)*

> **Read [What is testing](../what-is-testing/SKILL.md) first.** General rules for every phase: [test-session](../test-session/SKILL.md).

# QA skill variants (non-web products)

**When:** before a charter for a product that isn't a website or web app, for example an API, a command-line tool, a mobile app, an agent or a data pipeline. Targets you test by reading (skills, documents, a process) need no variant. The core skills give web examples; a variant swaps them for ones that fit.

## Never changes

The ethical and authorisation boundaries: the risky-probe gate and hard lines, secrets, resource cleanup on a shared computer, never changing the product's code or deciding what the product is meant to do, honesty about what was and wasn't done, the manager's confirmation of the charter before testing, and the self-review and retro at the end of every session (their shape can adapt; they can't be dropped). The principles stay too: success as useful, credible information about the mission; the bug definition; who matters (people and agents, equal in standing, each through its own means and oracles); questioning the brief; input matching the actor.

## Can adapt, with a reason

Everything else, including the coverage model, the workflow and its order, what evidence fits and how it is reviewed, the report, the retro's shape, and stopping arrangements agreed with the manager. Say what you adapted and why.

## Usually changes (examples)

1. **Driver:** what operates the product (for example a shell, an HTTP client, a device emulator, the agent's own chat).
2. **Target settings:** the conditions that change what users experience (for example OS and locale, API version and role, device and OS version, input data shape).
3. **Evidence and recording:** a capture with a clock you can trust (for example a timestamped terminal transcript, logged requests and responses).
4. **Access check:** the first thing a user would do (for example run the version command, call the base address).
5. **User actions:** what users can do or reasonably believe they can do (for example every flag the help lists, every endpoint and parameter the docs mention, every link a response returns).
6. **Safe versus risky:** which ordinary actions write real data (for example a POST to a live API is a write; a command run in a scratch folder you made is safe).
7. **Who-matters prompts:** who uses it, including agents (for example scripts that parse the output, client apps, downstream jobs).

## How to make one

1. Copy the core skills you need to `<name>-<kind>` (for example `run-test-session-cli`).
2. Change what the product needs, keeping the "Never changes" boundaries; note each adaptation and its reason in the copy.
3. Give the copy its own version line naming the core version it came from and what changed.
4. Send the manager a one-line summary of the changes and wait for them to confirm before the charter. Silence is not a yes.
5. In the retro, say whether the variant worked, so it can be improved.

## Worked examples (from a dry run on an API and a command-line tool)

- "Access check from a fresh signed-out profile" didn't fit: it became "run the version command with no credentials set" and "call the base address".
- "Evidence that fits the claim": the capture became the exact command and output, or the full request and response.
- Screen recording didn't fit: a timestamped terminal transcript or request log replaced it.
- The smoke-run "browser opens" became "the tool runs its version command".
- "Look at every screen": every command's help and output, every endpoint's responses.
- "Is a command that writes local files risky?": safe in a scratch folder you created; any write to a live API goes through the gate.
- Evidence review "every screenshot, any visual change": every capture, and any change in output a user or script would notice.

