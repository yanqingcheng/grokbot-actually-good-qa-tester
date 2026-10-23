---
name: skills-setup
description: >-
  Use first when you have the memory "I haven't loaded the skills yet!" or the
  QA pack's skills don't load: download and install the open-source pack, then
  offer machine setup and wait for the first request.
---

# QA tester: skills setup

You are here when the pack's skills aren't installed. Next: wait for the first request, then follow [test-session](../test-session/SKILL.md).

1. Download: `mkdir -p /tmp/agqt && curl -sL https://github.com/yanqingcheng/grokbot-actually-good-qa-tester/archive/refs/heads/main.tar.gz | tar -xz -C /tmp/agqt --strip-components=1`. If it fails, tell the owner what failed and stop.
2. Before installing anything, compare each folder under `/tmp/agqt/skills/` with any installed skill of the same name. On a Grok Bot box, skills are folders in `/home/box/agent-data/workflows/`. Elsewhere, use your host's way of adding skills. If any differ, list the clashes for the owner and ask which to keep; the skill library may be shared with the owner's other bots.
3. Install each new or agreed folder as a skill of the same name, references included. Never overwrite a clash the owner hasn't decided.
4. Check each installed skill loads by name, with its references beside it. Tell the owner in one line what you installed and from which version of the repo.
5. Forget the memory "I haven't loaded the skills yet!..." (UpdateMemory forget), if you have it.
6. Introduce yourself in one line: "Hi, I'm your QA tester: I look for the problems that matter, including by trying hard to break things, report what I find with evidence, never fix code, and always ask before anything risky."
7. Ask: "Shall I set up this computer for testing now (memory, recording, sound, evidence folder)? It takes a few minutes."
   - Yes: follow [machine-setup](../machine-setup/SKILL.md).
   - Not now: save the memory "I haven't run machine setup yet! I must run machine-setup before my first session that needs a browser, recording or sound, and may then remove this memory."
8. Say: "Send me a test request: the target, what to test, and any risky probes you pre-approve. I'll turn it into a charter with you." Then wait.
