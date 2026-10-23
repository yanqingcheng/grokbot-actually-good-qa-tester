---
name: machine-setup
description: >-
  Use when you have the memory "I haven't run machine setup yet!", or before a
  session needs a browser, recording or sound on a computer you haven't set up:
  memory floor, recording, sound, evidence folder, and proving the basic tools.
---

# QA tester: machine setup

You are here when this computer isn't set up for testing. Next: back to where you came from (skills-setup, or the session that needed it).

## 1. Reuse what's known

If your house rules or the owner's documentation say where machine notes for this computer live (another bot may have recorded them), read them first. Check each item still holds before you rely on it. Ask the owner only for what's missing or no longer true.

## 2. Settle

1. Memory floor: how much free memory the computer must have before you start a browser, server or recording.
   - Use a limit from the house rules or owner, with its reason.
   - With none, measure what the browser and recorder use and propose a margin above that.
2. Recording: suggested, a screen grab with a clock burned in, or the browser's own screencast when headless, and sound from the computer's audio output. Confirm with the owner.
3. Evidence folder root: suggested `<your workspace>/qa/`, with a subfolder per project and a dated folder per session. Confirm with the owner.

## 3. Prove your tools

1. Read `test-session/references/session-rules.md`, `test-session/references/targets-and-evidence.md`, `test-session/references/resource-cleanup.md` and any house rules. Check memory against the floor and take any lease required.
2. Prove for real, on something harmless you control (a blank page, a small local page that plays a sound): driving a browser, a phone-sized screen with touch, recording the screen with a clock, recording sound, getting a recording reviewed. Never use a real product nobody asked you to test.
3. Keep the proof (a short clip, a sound file with a level reading).
4. Clean up as the session rules say.

On a Grok Bot box, use `machine-setup/references/grok-bot-box.md` for driving Chrome, recording with a clock, leases and secrets, and `machine-setup/references/grok-bot-box-sound.md` for sound and speech voices. On other hosts, skip them.

## 4. Save

1. Save the floor (with its reason or measurement), the recording method and the evidence folder root to memory, and in the machine notes where the house rules say.
2. Note what works, how you proved it and what's missing. Tell the owner in one line. A missing capability the work needs is a finding: ask for it.
3. Forget the memory "I haven't run machine setup yet!..." (UpdateMemory forget), if you have it.
