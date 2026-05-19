# Copilot instructions — repository-level

Purpose
Provide concise, repository-specific guidance so Copilot CLI agents and future contributors understand the repo layout, file formats, and how to make safe edits.

Build / test / lint
No explicit build, test, or lint commands were detected in this repository at the time of this update. If a build or test system is added, include runnable commands here and an example to run a single test (for example: `npm test -- <test-name>` or `pytest -k <test-name>`).

Repository overview
- Primary files: `AGENTS.md`, `Modelfile`, `README.md`.
- Purpose: learning and experimenting with Copilot/agent workflows and custom agents.

File format & conventions
- Encoding: UTF-8.
- Line endings: LF (Unix-style).
- Paths: use forward slashes (`/`) and workspace-relative paths when referencing files in text or patches.
- When editing files, prefer minimal, focused diffs that preserve unrelated code and metadata.

Agent guidance (for Copilot CLI / subagents)
- Keep responses concise and actionable.
- Use POSIX-style workspace-relative paths (forward slashes) when referencing files (e.g., `src/main.py`).
- When proposing or performing edits, always:
  1. Show the exact files changed and the exact diff or replacement text (use unified diff or apply_patch-style hunks).
  2. Preserve file encoding and important header lines.
  3. Apply matching edits to related files in the same change to keep the repository consistent.
  4. For non-trivial changes, show one or two verification commands that users can run locally (e.g., `git --no-pager diff`, `grep -n "TODO" src/`).
- If your change requires running tests, state that and provide the command to run them; do not run tests unless asked or unless you have explicit permission.
- When the repository contains agent/config files (for example `AGENTS.md`), prefer referring to them and keeping them in sync when changing agent behavior.

How to change agent response style
- Repository-level: edit this file to suggest defaults for agents working in this repo.
- User-level: users can create a per-user preferences file at `$HOME/.copilot/copilot-instructions.md` (Linux/macOS) or `%USERPROFILE%\\.copilot\\copilot-instructions.md` (Windows).
- Example block to add at the top of a preferences file:

  Response style: Keep replies concise (<=100 words). Use a professional tone. Prefer bullet lists for steps. Use workspace-relative forward-slash paths.

Other AI assistant configs checked
- Found: `AGENTS.md` in the repository root. Keep that file authoritative for agent lists and agent-specific instructions.

Notes for contributors and agents
- Preserve repository structure and avoid renaming top-level files without coordination.
- When making multi-file edits, group them into a single commit/PR and include an explanatory commit message.
- If you find the instructions here are no longer accurate, update this file and mention the change in the PR description.

Contact / follow-up
If you want, I can:
- Update `AGENTS.md` to reflect current agent workflows.
- Add a short `CONTRIBUTING.md` with repository-specific developer steps.
Tell me which of these you'd like next.
