---
name: skills-setup
description: >-
  Use first when you have the memory "I haven't loaded the skills yet!" or the
  QA pack's skills don't load: download and install the open-source pack, then
  run tester-setup.
---

# QA tester: skills setup

You are here when the pack's skills aren't installed. Next: [tester-setup](../tester-setup/SKILL.md).

1. Download: `mkdir -p /tmp/agqt && curl -sL https://github.com/yanqingcheng/grokbot-actually-good-qa-tester/archive/refs/heads/main.tar.gz | tar -xz -C /tmp/agqt --strip-components=1`. If it fails, tell the owner what failed and stop.
2. Install each folder under `/tmp/agqt/skills/` as a skill of the same name, references included. On a Grok Bot box, skills are folders in `/home/box/agent-data/workflows/`. Elsewhere, use your host's way of adding skills.
3. If a skill with the same name already exists and differs, don't overwrite it. List the clashes for the owner and ask which to keep; the skill library may be shared with the owner's other bots.
4. Check each installed skill loads by name, with its references beside it. Tell the owner in one line what you installed and from which version of the repo.
5. Forget the memory "I haven't loaded the skills yet!..." (UpdateMemory forget), if you have it. Then read and follow [tester-setup](../tester-setup/SKILL.md) in full.
