---
apply-to: .github/agents/*.agent.md
---

## Purpose
This document is a go-through instruction set for creating, reviewing, and maintaining Duck Creek custom-agents for the project. It defines a strict, repeatable template, required metadata, verification steps, and a lightweight workflow to ensure consistency.

## Scope
Applies to all custom-agent files under `.github/agents/` (see `apply-to` in this instruction file's frontmatter). Use POSIX-style paths and workspace-relative references in all edits.

## Required template
Every agent file MUST include the following sections (in this order) and use the YAML frontmatter shown in the example below:

- Frontmatter (required fields):
	- `id`: unique kebab-case id, e.g. `duck-claim-review`
	- `name`: human-friendly name
	- `version`: semver (e.g. `0.1.0`)
	- `author`: GitHub username or team

- Body sections (required):
	1. `Description` — short summary of what the agent does.
	2. `Purpose` — why it exists and the scope of responsibility.
	3. `Patterns and Syntax` — canonical input patterns, example tokens, and any parsing rules.
	4. `Examples` — minimal input → expected output pairs (both happy-path and common edge cases).
	5. `Constraints / What Not To Do` — explicit forbidden actions and risky behaviors.
	6. `Verification Steps` — tests and manual checks to validate the agent.
	7. `Response Style` — tone, length limits, and formatting rules.
	8. `Changelog` — brief history of edits (date, author, short note).

### Minimal frontmatter example
```
---
id: duck-claim-review
name: Duck Claim Review Agent
version: 0.1.0
author: @team-duck
---
```

## How to create a new agent (step-by-step)
1. Create a new file under `.github/agents/` named `<id>.agent.md` using kebab-case for `id` and the same `id` in frontmatter.
2. Populate the required sections and include at least 3 `Examples` covering happy path, one edge case, and one invalid input.
3. Document the set of input patterns in `Patterns and Syntax` and reference repository locations where those patterns were observed.
4. Add `Verification Steps` describing automated tests (if available) and at least one manual check.
5. Open a PR with the new file. The PR description must include: what the agent does, how to test it locally, and the verification checklist.

## Pattern coverage requirement
- Before marking an agent ready for review, document representative patterns that cover the agent's expected workload. Aim to document at least 60% of common input variations via `Examples` and `Patterns and Syntax` (this is a documentation threshold, not a hard ML metric).

## Iteration strategy
- Start small: ship a minimal working agent that follows the template and passes the verification checklist.
- Iterate by expanding `Patterns and Syntax` and `Examples`, and by adding automated tests where feasible.

## Single Responsibility
- Each agent should have a focused responsibility. If a task naturally decomposes into sub-tasks, implement separate agents that coordinate via clearly documented handoffs.

## Verification checklist (PR template)
- Frontmatter present and valid.
- At least 3 examples provided.
- Patterns documented and source locations referenced.
- Manual verification steps listed and reproducible.
- Response style defined and conforms to project voice.
- Changelog entry added.

Suggested PR verification commands (copy-paste):
```bash
git --no-pager diff --staged
grep -n "^id: \|^name: \|^version: " .github/agents/*.agent.md
``` 

## Review and enforcement
- Reviewers must verify the checklist and can request changes. Merge only after an approving review.
- Keep `Changelog` entries for any subsequent edits and bump `version` following semver rules for non-trivial changes.

## Style and response rules
- Preferred tone: professional, concise, and factual.
- Max answer length for user-facing replies: 200 words unless otherwise specified.
- Use explicit code blocks for examples and outputs. Prefer JSON or YAML when exchange formats are structured.

## Contact
For questions about conventions or reviews, ping `@team-duck` on the repository or open an issue titled `agent-convention: <short-description>`.
