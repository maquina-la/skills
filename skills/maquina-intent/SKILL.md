---
name: maquina-intent
description: Create and maintain a scoped Máquina work intent for an agent-assisted software-delivery task. Use when beginning implementation, planning a pull request, recovering a PR that lacks Máquina linkage, or defining allowed paths, acceptance criteria, and validation context before an agent edits code.
---

# Máquina intent

Create one small, task-specific intent before implementation. Treat the intent as the declared boundary for the work—not as a retrospective summary.

## Workflow

1. Read the repository's `AGENTS.md` and `.maquina/factory-contract.json` when present.
2. Choose the next unused identifier using the repository's existing naming convention.
3. Create `.maquina/intents/<ID>-<short-slug>.json` using the schema in [intent format](references/intent-format.md).
4. Keep `allowed_paths` narrow and literal. Include only paths that are genuinely necessary.
5. Add measurable acceptance criteria and the smallest relevant context references.
6. Validate the JSON. If the repository has the Máquina CLI, run `maquina contract validate` from the repository root.
7. Attach these lines to the pull-request description exactly:

   ```text
   Maquina-Intent: .maquina/intents/<intent-file>.json
   Maquina-Work-Type: <work-type>
   Maquina-Validation-Profile: <profile>
   ```

Do not broaden an existing intent merely to make a diff pass. Split unrelated work into another intent.

## Safety

- Never put source code, credentials, user data, prompts, or raw model output in an intent.
- Do not claim validation, deployment, or business outcomes as completed unless they were observed.
- If the PR changes a protected resource, state that fact in the intent and follow the Factory Contract's approval rule.
