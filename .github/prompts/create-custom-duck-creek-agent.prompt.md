# Create Custom Duck-Creek Agent

Purpose: guide a user through creating a new Duck-Creek agent that follows repository conventions, uses relevant tools, and reuses patterns from known DCT templates.

Required: every new agent must follow the instructions in `.github/instructions/duck-agents.instrcutions.md` and—when requested—should fetch patterns from the project templates folder:

- Templates folder (source of patterns): E:\CNF\DCT Files\ManuScripts\ManuScripts\DCTTemplates

Process (what the prompt asks the user and what the system will do):

1) Collect basic inputs from the user
- Agent name: concise, PascalCase, 1–4 words
- Agent description: 1–3 sentences describing purpose, target users, and primary capabilities
- Primary role/task: single sentence describing the role (e.g., `underwriter-assistant`, `policy-validator`)

2) Tools discovery and selection
- Ask the user to list required tools (APIs, scripts, CLI commands, file readers). If they omit tools, the AI should propose a minimal tool set tailored to the role.
- Example tool categories to suggest: `document_reader`, `template_fetcher`, `policy_extractor`, `rule_validator`, `compliance_lookup`, `duckcreek_cli_adapter`.

3) Template scanning (optional but recommended)
- Offer to scan the templates folder for relevant patterns and examples, and list the templates that will be used to seed agent behavior.
- If the user agrees, the agent should read from the path above and summarize matching templates (names, purpose, example snippets).

4) Compliance with repository instructions
- Confirm that the generated agent file will follow `.github/instructions/duck-agents.instrcutions.md` and include a `compliance` block that references that instructions file.

Output: produce a ready-to-save agent configuration file containing the following fields (JSON/YAML preferred):

- `name`: string (PascalCase)
- `description`: string
- `role`: string
- `model`: string (suggest default if user omits)
- `tools`: array of objects { `name`, `signature`?, `description`, `required`: boolean }
- `templates_used`: array of template file names (populated if scanning requested)
- `compliance`: { `instructions_path`: ".github/instructions/duck-agents.instrcutions.md", `checked`: true }

Example flow (minimal):

User provides:
- name: FieldAgent
- description: Expert in duck creek manuscript field creatioon and modification.
- role: Creating and modifying field in duck creek manuscripts.

AI returns (example snippet):

```json
{
  "name": "FieldAgent",
  "description": "Assists field staff in extracting coverage terms and generating summaries from policy templates.",
  "role": "field-data-extraction",
  "model": "gpt-4-turbo",
  "tools": [
    {"name":"document_reader","description":"Reads policy and template files from disk","required":true},
    {"name":"policy_extractor","description":"Extracts policy terms and coverage info","required":true}
  ],
  "templates_used": ["policy_template_A.dct","summary_template.md"],
  "compliance": {"instructions_path":".github/instructions/duck-agents.instrcutions.md","checked":true}
}
```

Prompt guidance for the assistant implementing this prompt
- When the user omits tools, suggest a minimal, role-specific set and explain why each is needed.
- When scanning templates, only list files and short snippets; do not copy full proprietary templates unless user explicitly requests it.
- Always include the `compliance` block referencing `.github/instructions/duck-agents.instrcutions.md`.
- If the templates path is inaccessible, explain the limitation and ask the user to provide a zipped archive or grant access.

User-facing checklist (questions to ask the user)
- What is the agent name?
- Provide a short description (1–3 sentences).
- What role or task should the agent specialize in?
- Which tools or APIs should the agent be allowed to use? (leave blank to get suggestions)
- Allow scanning of templates at E:\CNF\DCT Files\ManuScripts\ManuScripts\DCTTemplates? (yes/no)

End of prompt.
