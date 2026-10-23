---
name: machine-setup
description: >-
  Use when you have the memory "I haven't run machine setup yet!", or before a
  session needs a browser, recording or sound on a computer you haven't set up:
  memory floor, recording, sound, evidence folder, and proving the basic tools.
---

# QA tester: machine setup

You are here when this computer isn't set up for testing. Next: back to where you came from (skills-setup, or the session that needed it).

## Why

Your reports are only as good as your evidence. You need to capture honestly what a real person sees and hears when they use the product, at a time you can trust, without harming a computer other people and bots may share. Everything below serves that.

## What you need to be able to do

1. Leave the computer healthy: know how much free memory it needs before you start a browser, server or recording (the memory floor), take any lease it requires, and clean up only what you started.
2. Use the product as its actors do: drive a real browser, at desktop size and at phone size with touch.
3. Show what happened and when: record the screen with a trustworthy clock in the picture.
4. Hear what a person would hear, when the product makes sound: record sound you can attribute to your own browser.
5. Check your own evidence: review a recording yourself (or have it reviewed) before you rely on it.
6. Keep evidence where it can be found: one evidence folder root ("Evidence folder" in `test-session/references/targets-and-evidence.md`).

## Where the specifics come from

1. Read `test-session/references/session-rules.md`, `test-session/references/targets-and-evidence.md`, `test-session/references/resource-cleanup.md` and any house rules first.
2. This computer's specifics (memory floor and its reason, lease tool, sound server, recorder, evidence root) come from your house rules and any machine notes they or your owner point to (default `<evidence folder>/machine-notes.md`; another bot may have recorded them). Where they say nothing, find out by probing the computer yourself, and propose values to the owner.
3. Read your saved machine state too. Check each item still holds before you rely on it.
4. Machine choices belong to this computer's owner, not to whoever requested a session. Ask the owner only for what's new, missing or no longer true; if a requester isn't the owner, tell them what you're waiting on.
5. Memory floor with no rule: check free memory, take any lease, then measure one harmless browser page and a short recording, stop them, and propose a margin above that.

## Prove your tools

Show each ability for real, on something harmless you control (a blank page, a small local page that plays a sound). Prove it the way a session will use it: sound proof is a sound played by the browser you test with and captured as a session would, not a tone played straight into the speaker. Never use a real product nobody asked you to test. Work in `<evidence folder>/machine-setup/<YYYY-MM-DD>/` as your session folder, with a `notes.md`, and keep the proof there (a short clip, a sound file with a level reading). Check memory against the floor and take any lease first; clean up as the session rules say.

- A proof that fails, or a tool that isn't there, is a recorded gap, not a reason to pretend: note what you tried and what's missing, and tell the owner.
- Review a recording yourself: extract at least three frames, from its start, middle and end, look at each one, and check the burned-in clock against your log times. Note who reviewed it.

On a Grok Bot box, `machine-setup/references/grok-bot-box.md` has recipes for driving Chrome and recording with a clock, and `machine-setup/references/grok-bot-box-sound.md` for sound and speech voices. Your house rules give the box's own paths and lease tool. On other hosts, skip them.

## Save

1. Save the floor (with its reason or measurement), the recording method and the evidence folder root to memory, and in the machine notes: where the house rules say, otherwise `<evidence folder>/machine-setup/<YYYY-MM-DD>-<your name>/notes.md` (other bots may set up the same day) with a summary at the top, linked from `<evidence folder>/machine-notes.md` (the stable path other bots read).
2. Save the machine state: what's proven (with the proof folder) and what's missing. Tell the owner in one line. A missing capability the work needs is a finding: ask for it.
3. If you have the memory "I haven't run machine setup yet!...", replace it: with nothing missing, forget it (UpdateMemory forget); otherwise update it to "Machine setup ran <date>; missing: <gaps>; proof: <folder>. Re-check these before a session that needs them."
