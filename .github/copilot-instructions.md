# Copilot instructions — repository-level

Purpose
Provide repository-specific guidance so Copilot CLI agents and future contributors understand the repo layout, file formats, and how to make safe edits.

Build / test / lint
No explicit build, test, or lint commands were detected in this repository. If a build or test system is added, include runnable commands here and examples to run a single test (for example: `npm test -- <test-name>`).

Repository overview
- This repository stores two plain-text data tables used as simple item storage:
  - `item_names.txt` — header line: `ItemName` followed by one item name per line.
  - `item_prices.txt` — header line: `ItemPrice` followed by one numeric price per line.
- Files are intended to remain line-aligned: the Nth data line in item_names.txt corresponds to the Nth data line in item_prices.txt.

File format & conventions
- Encoding: UTF-8
- Line endings: CRLF (Windows)
- Header lines must be preserved exactly: `ItemName` and `ItemPrice`.
- Prices: use plain decimal notation (e.g., 12.50). Do not include currency symbols in the data file.
- When adding or removing an item, update both files in the same change so line alignment is preserved.

Agent guidance (for Copilot CLI / subagents)
- Keep responses concise and actionable.
- Use Windows-style paths (backslashes) when referencing files.
- When proposing or performing edits to these data files, always:
  1. Show the exact files changed and the exact diff or replacement text.
  2. Preserve header lines and encoding.
  3. If adding/removing items, apply matching edits to both files in one commit/PR.
  4. For non-trivial changes, show the commands used to verify the change (e.g., `type "E:\\AI Projects\\CopilotTraining\\item_names.txt"`).
- If using fleet/agent todos, update the session todos table (if present) after completing work.

How to change agent response style
Edit this file or create a user-level file at `%USERPROFILE%\\.copilot\\copilot-instructions.md`. To prefer concise replies and Windows-paths, add a short `Response style:` block at the top, for example:

Response style: Keep replies concise (<=100 words). Use a professional tone. Prefer bullet lists for steps. Use Windows paths and show changed files.

Other AI assistant configs checked
- No CLAUDE.md, AGENTS.md, CONVENTIONS, or other known assistant config files were detected in the repository root.

