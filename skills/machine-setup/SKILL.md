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

1. Read `test-session/references/session-rules.md`, `test-session/references/targets-and-evidence.md`, `test-session/references/resource-cleanup.md` and any house rules.
2. Read your saved machine state and any machine notes the house rules or owner's documentation point to (another bot may have recorded them). Check each item still holds before you rely on it.
3. Machine choices belong to this computer's owner, not to whoever requested a session. Ask the owner only for what's new, missing or no longer true; if a requester isn't the owner, tell them what you're waiting on.

## 2. Settle

1. Memory floor: how much free memory the computer must have before you start a browser, server or recording.
   - Use a limit from the house rules or owner, with its reason.
   - With none, check free memory, take any lease, then measure one harmless browser page and a short recording, stop them, and propose a margin above that.
2. Recording: suggested, a screen grab with a clock burned in, or the browser's own screencast when headless, and sound from the computer's audio output. Confirm with the owner.
3. Evidence folder root: keep the one already set ("Evidence folder" in `test-session/references/targets-and-evidence.md`), otherwise suggest `<your workspace>/qa/`. Confirm with the owner.

## 3. Prove your tools

1. Work in `<evidence folder>/machine-setup/<YYYY-MM-DD>/` as your session folder, with a `notes.md`. Check memory against the floor and take any lease required.
2. Prove for real, on something harmless you control (a blank page, a small local page that plays a sound): driving a browser, a phone-sized screen with touch, recording the screen with a clock, recording sound, getting a recording reviewed. Never use a real product nobody asked you to test.
3. Keep the proof there (a short clip, a sound file with a level reading).
4. Clean up as the session rules say.

On a Grok Bot box, use `machine-setup/references/grok-bot-box.md` for driving Chrome, recording with a clock, leases and secrets, and `machine-setup/references/grok-bot-box-sound.md` for sound and speech voices. On other hosts, skip them.

## 4. Save

1. Save the floor (with its reason or measurement), the recording method and the evidence folder root to memory, and in the machine notes where the house rules say.
2. Save the machine state: what's proven (with the proof folder) and what's missing. Tell the owner in one line. A missing capability the work needs is a finding: ask for it.
3. If you have the memory "I haven't run machine setup yet!...", replace it: with nothing missing, forget it (UpdateMemory forget); otherwise update it to "Machine setup ran <date>; missing: <gaps>; proof: <folder>. Re-check these before a session that needs them."
