# Resource cleanup

Part of [test-session](../../test-session/SKILL.md). Open before you start a browser, dev server or recording, before taking a lease, and at the end of every session. Every-phase rules: `test-session/references/session-rules.md`.

## Resource cleanup (leave the computer as you found it)

- Before you start: run `free -m`. If available memory is under your memory floor (from machine setup), tell the manager and hold before starting a browser, dev server or recording. Prefer a cloud runner for long or heavy runs.
- Track what you start. Every background process you launch (recorder, logger, poller, watcher, dev server) writes a pid file in the session folder (`video/rec-01.pid`) and gets a line in `notes.md`. A process your own script starts and stops needs no pid file, but the script must stop it even when it fails, and `notes.md` records that it ended. Close every tab or window you open.
- Leases and locks. Follow your host's resource lease, if it has one, as its docs or house rules say. Grok Bot box commands: "Leases" in `machine-setup/references/grok-bot-box.md`. Name the holder after this run (`<your name>-<session folder name>`) so two of your runs never release each other's lease. Release by lease id or this run's holder name.
- Waiting for a lease: wait your turn. Log the wait's start and end in `notes.md`. Do safe work that needs no browser meanwhile. If the wait puts the mission or timing at risk, ask the manager whether to keep waiting.
- **Stop only your own processes, by pid.** Never by a name or pattern another session could share. If something else hogs memory, report it.
- Run only helpers you own and track, within measured capacity and lease limits. Stop each when its probe reports back.
- At the end of every session (after the evidence review, before the report), and if you stop early, fail or time out:
  1. Check every script you ran has ended. For each pid file, stop the process (`kill -INT` for recordings, so the file finalizes) and confirm with `ps` it is gone. If the pid was a wrapper shell, find the real process by your own file's full path, check it is yours, and stop it by pid. Close Playwright contexts. Do this before releasing any lease.
  2. Close the browsers, tabs and windows you opened. Leave at most one blank tab.
  3. Delete scratch files you created outside the evidence folder (downloads, temp builds, extracted frames, virtualenvs).
  4. Keep `charter.md`, `notes.md`, `report.md`, `retro.md`, `shots/`, the clips the report cites, and every file the brief or these skills require. Delete unused or duplicate recordings. Re-encode long clips smaller if needed.
  5. Release every lease or lock you took.
  6. Run `free -m` again and write one "cleanup done" line in `notes.md`: each pid file and whether its process is gone, what you deleted, memory before and after. Copy it into the report. If you stop early with no report, send it to the manager.
