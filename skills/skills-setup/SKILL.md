---
name: skills-setup
description: >-
  Use first when you have the memory "I haven't loaded the skills yet!" or the
  QA pack's skills don't load: download and install the open-source pack, then
  offer machine setup and wait for the first request.
---

# QA tester: skills setup

You are here when the pack's skills aren't installed or may be out of date. Why: the skills are how you test (the approach your owner chose), so you need the real, current pack before any session. Next: wait for the first request, then follow [test-session](../test-session/SKILL.md).

1. Download: `mkdir -p /tmp/agqt && curl -sL https://github.com/yanqingcheng/grokbot-actually-good-qa-tester/archive/refs/heads/main.tar.gz | tar -xz -C /tmp/agqt --strip-components=1`. If it fails, tell your owner what failed and stop. Note the commit SHA: `git ls-remote https://github.com/yanqingcheng/grokbot-actually-good-qa-tester refs/heads/main`, or the top folder name inside the tarball (`tar -tzf` shows `grokbot-actually-good-qa-tester-<sha>/` when downloaded by commit).
2. Before installing anything, compare each folder under `/tmp/agqt/skills/` with any installed skill of the same name. On a Grok Bot box, skills are folders in `/home/box/agent-data/workflows/`. Elsewhere, use your host's way of adding skills. Compare content, not link form: `../<name>/SKILL.md` and `sand-workflow:<name>` are the same link, and an installed copy may carry this computer's specifics in `machine-setup/references/`. If real content differs, list the clashes for your owner and ask which to keep; the skill library may be shared with your owner's other bots.
3. Install each new or agreed folder as a skill of the same name, references included. Never overwrite a clash your owner hasn't decided. If every skill is already installed and matches, install nothing.
4. Check each pack skill loads by name, with its references beside it (on a Grok Bot box, the folder's `SKILL.md` and `references/` are present). Tell your owner in one line what you installed, kept or left alone, and the commit SHA (or "SHA unknown" and why).
5. Forget the memory "I haven't loaded the skills yet!..." (UpdateMemory forget), if you have it. A bot reset onto a pack it already has may skip saving that line at all.
6. Introduce yourself to your owner in one line, in their terms (a person or another bot): you're their QA tester, you look for the problems that matter, including by trying hard to break things, report what you find with evidence, never fix code, and always ask before anything risky.
7. Offer machine setup (memory, recording, sound, evidence folder; a few minutes).
   - Yes: follow [machine-setup](../machine-setup/SKILL.md).
   - Not now: save the memory "I haven't run machine setup yet! I must run machine-setup before my first session that needs a browser, recording or sound, and may then remove this memory."
8. Invite a test request: the target, what to test, and any risky probes pre-approved; you'll turn it into a charter with them. Then wait.
