# Targets and evidence

Part of [test-session](../../test-session/SKILL.md). Open at setup and before the access check. Every-phase rules: `test-session/references/session-rules.md`.

## Targets, access and accounts

- Target: the charter names it (a site or web app, preview or live, or a reading target: skills, a document, a process) and how to get access. A practice target only exercises the thing under test. Report its bugs separately. Live is not a stand-in for a preview.
- Access check: before you send the charter, a read-only check with no saved login (`curl` or equivalent) that reaches the right version is enough. Browser proof comes at the first smoke run, inside your lease, as its first step. Record one result:
  - reachable.
  - reachable, browser check at smoke run: say what is unchecked. Record any failure at the smoke run and its scope.
  - unreachable: tell the manager the blocker and the scope it affects.
- Test accounts: use only accounts the manager or PO provides or approves.
- Secrets: "Secrets" in `test-session/references/session-rules.md`.

## Evidence folder

The evidence folder root comes from the house rules or your memory. With neither, use `<your workspace>/qa/`, save it to memory and tell the owner in one line. Settle it before writing any project file.

`<evidence folder>/<project>/` holds `setup.md` and one session folder per session, `<YYYY-MM-DD>-<your name>/`. Create it so that it fails if it exists (`mkdir`, never `mkdir -p`), and on failure add a suffix (`-2`) and try again. Never write into a folder you didn't create: another tester's files would be overwritten. If the brief or house rules name folders differently, follow them and raise any collision. A session folder holds `charter.md`, `notes.md` (session sheet, with its Bugs section), `report.md`, `retro.md`, `shots/` and `video/`. Keep it where your video reviewer can read it.

Shared storage (if house rules ask): add only your own session's files, record yourself as author, and if it is in an unexpected state, leave it and tell the manager.

