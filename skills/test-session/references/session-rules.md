# Session rules: resource cleanup and the risky-probe gate

Part of [test-session](../../test-session/SKILL.md). Read before your first charter, and again before any cleanup or risky probe.

## Resource cleanup (leave the computer as you found it)

- **Before you start:** run `free -m`. If available memory is under **your memory floor (from setup)**, tell the manager and hold (or ask) before starting a browser, dev server or recording. Prefer a cloud runner for long or heavy runs.
- **Track what you start.** You must be able to stop everything you start and show it stopped. Every background process you launch (recorder, logger, poller, watcher, dev server) writes a pid file in the session folder (for example `video/rec-01.pid`, `dev-server.pid`); also note it in `notes.md`. Things that run inside your own script (illustration: a recorder started and stopped by the script) need no pid file, but the script must stop them when it ends, including when it fails, and `notes.md` records that it ended. Close every browser tab or window you open.
- **Shared locks and leases.** If your environment makes you take a lease or lock, name the holder after this run, not just after you, for example `<your name>-<session folder name>`. Two runs of the same tester then never share, reuse or release each other's lease. Release by lease id, or by this run's holder name.
- **Waiting for a lease.** If the lease or tool you need is busy (refused, or held by another run, including another run of yours that the brief says to wait for), wait your turn rather than squeezing in: log when the wait starts and ends in `notes.md`, do safe work that needs no browser meanwhile (charter, notes, reading), and retry when the resource is likely to be free (the holder's release, your host's retry policy, or a check that is cheap compared with the time left). Waiting time is logged but doesn't count against the timebox. Everything else in the session counts, including research, planning and reflection, because they are part of testing (as in step 10 of [run-test-session](../../run-test-session/SKILL.md) and `references/stopping-heuristics.md`). If the wait starts to put the session's mission or timing at risk, tell the manager and ask whether to keep waiting (illustration: a wait as long as the session itself is a good point to ask, or sooner for a short round).
- **Stop only your own processes.** Never kill a process you did not start. If something else looks like it is hogging memory, report it to the manager instead.
- **At the end of every session (after the evidence review, before the report), and also if you stop early, fail or time out:**
  1. Check that every script you ran has ended and nothing it started is still running. For every pid file in the session folder, stop that process (`kill -INT` for recordings, so the file finalizes) and confirm it is gone with `ps`; if the pid belonged to a wrapper shell, find the real process by the full path of your own session's file, check it is yours, and stop it by its pid; never stop anything by a name or pattern another session could share. Also close Playwright contexts. Do this before ending the session or releasing any lease.
  2. Close the browsers, tabs and windows you opened. Leave at most one blank tab.
  3. Delete scratch files you created outside the evidence folder (downloads, temp builds, extracted frames, virtualenvs).
  4. Keep `charter.md`, `notes.md`, `report.md`, `retro.md` (written after the report), `shots/`, the `video/` clips the report cites, and every other file the brief or these skills require (for example a separate bug list or a run log). Delete only scratch and unused material. Delete unused or duplicate recordings, and re-encode long clips smaller if needed.
  5. Release any resource lock or lease your environment asked you to take (by id, or by this run's holder name; never by a name another run might share).
  6. Run `free -m` again and write a one-line "cleanup done" note (each pid file and whether its process is confirmed gone, what was deleted, memory before and after) in `notes.md`; copy it into `report.md` when you write the report, just before the final one-line verdict (the verdict stays last). If you stop early and there is no report, send that line to the manager.
- **Run only the helpers you own and track, within the computer's measured capacity and any lease limits** (your house rules may set a count), and never leave one running in the background after its probe reports back.

## Risky-probe gate (applies at charter time and mid-session)

**Risky** = any of:
- testing a live or production target, meaning anything real users or real data depend on (not a preview);
- destructive or irreversible actions: deleting/wiping data, mass-creating records, corrupting saved state;
- anything that sends real email, SMS, messages, or posts to real people or third parties. Opening something that only prepares a message is not a send (illustration: a `mailto:` link opens a draft in a mail app): opening it to see what it does is an ordinary user action, but sending it needs approval;
- payments or purchases;
- load, flood, or rate-limit hammering;
- security probing beyond normal UI input (e.g. injection payloads against a live backend);
- anything that could cost money or affect real users;
- anything else your owner listed as risky at setup (check your memories; if getting-started never ran and you have no saved list, ask the manager before the first session).

**Risk is judged by what an action could do, not by the target's label.** Anything on the risky list above stays risky on a preview too: a preview can still send real email, charge real money, share data with the live product or call paid services. If you don't know whether a preview is cut off from those, find out (ask the manager) before relying on it.

**Safe, no approval needed:** normal plus abusive (deliberately malformed, huge or hostile) input through the product's normal interface on a preview whose effects stay inside it (nothing in the risky list can happen), edge cases, tours, evidence capture, recording, and the ordinary actions a user would take on any target, including a live one once it is okayed or named in the request, because success needs them (examples: clicks, scrolling, navigation, playing media or games without saving). On a live target, **read-only** means no submits, sends, purchases or writes to real data that you choose to make; it never means page loads only. Anything the product records by itself for every visitor who simply uses it (illustrations: a visit counter, analytics, a "last seen" time) is part of ordinary use, not a risky write: it is safe, note it in `notes.md` as a side effect, and keep it to what the session needs (no repeated loads just to move a number). Following the product's links to other sites is a user action too: one ordinary click per link, which also counts as that link's check. If you're unsure whether an action writes real data beyond that, ask the manager; carry on with other safe work while you wait, and never skip it silently.

**Gate procedure** (before any risky probe, at charter time or mid-session):
1. List each planned risky probe: **what, where (address or area), why, worst case, how to undo.**
2. Message the manager (a bot: your bot-to-bot message tool, marked urgent if it can be, for example `SendToAgent` with priority true; a person: their agreed channel) and wait for an explicit okay.
3. Run only the probes they okay, exactly as scoped. An okay covers only the named probes, for this session.
4. While you wait, carry on with safe work. Agree with the manager, when you ask, when the decision is needed; if it hasn't come by then, remind them through the agreed channel, as often as the cost of the delay justifies. A decline means skip it. No answer by the end of the session also means skip it; never treat silence as a yes. Record "not run: approval declined" or "not run: approval pending".
5. Probes pre-approved in the original request count as okayed, as scoped there. A request that names a live target and limits how to use it (for example "live site, read-only") pre-approves exactly that; say so in the charter's gate list. A request that names a live target with no limits pre-approves read-only use (as defined under "Safe, no approval needed" above); anything more on live goes through the gate.

**Hard lines, even with approval:** never use the owner's real personal credentials or payment methods; never message real people outside the test: no messages to real recipients through the product under test or as part of a probe. Coordinating with your manager or the people the charter names, and delivering reports to the destination agreed at setup, are part of the job and not covered by this line.

