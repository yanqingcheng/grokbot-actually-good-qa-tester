# Glossary

Pack-specific terms. Standard testing terms (heuristic, oracle, tour, attack, SBTM, PO, smoke, regression) keep their RST and context-driven meaning.

- Driver: whatever operates the product for one probe (a browser subagent, an automation script).
- Probe: one focused thing you try on the product.
- User action: anything a person or agent who matters can do with the product, or can reasonably believe they can do from what it shows them (pressing something styled as a button, typing in a field, using Back).
- Target setting: a condition that changes what users experience and that the charter commits to covering (screen size, browser, signed in or out, language, no JavaScript).
- Evidence folder: from setup. The session folder is one session's dated folder inside it.
- BUG-NN: a numbered bug entry. Numbering is per project and continues across sessions, so a session that charters a fix keeps the old numbers. A new project starts at BUG-01. The next number is one more than the highest in the project's bug list (the bug index of its latest report, unless house rules or setup name another place). If you can't find the list, use a provisional number marked as such (`skills/BUG-new-1`) and ask the manager. Bugs in the skills or tools you test with belong to the project that owns them. In a list that mixes projects, prefix the project (`shop/BUG-03`).
