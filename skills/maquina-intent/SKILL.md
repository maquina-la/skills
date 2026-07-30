---
name: maquina-intent
description: Create and maintain a scoped Máquina work intent for an agent-assisted software-delivery task. Use when beginning implementation, planning a pull request, recovering a PR that lacks Máquina linkage, or defining allowed paths, acceptance criteria, and validation context before an agent edits code.
---

# Máquina intent

Create one small, task-specific intent before implementation. Treat the intent as the declared boundary for the work—not as a retrospective summary.

## Workflow

1. Read the repository's `AGENTS.md` and `.maquina/factory-contract.json` when present.
2. Choose the next unused identifier using the repository's existing naming convention.
3. Prefer the repository's Máquina CLI when it supports `intent create`:

   ```bash
   maquina intent create \
     --id TEAM-123 \
     --title "Short outcome-oriented title" \
     --objective "What will change and why." \
     --work-type backend \
     --allow service/handler.go \
     --context AGENTS.md \
     --accept "A specific observable outcome."
   ```

   Use the JSON shape in [intent format](references/intent-format.md) only when that command is unavailable.
4. Keep `allowed_paths` narrow and literal. Include only paths that are genuinely necessary.
5. Add measurable acceptance criteria and the smallest relevant context references.
6. Validate the contract. Run `maquina contract validate` from the repository root when the CLI is available.
7. Run `maquina intent metadata --input .maquina/intents/<intent-file>.json` when available, then attach its emitted intent/work-type lines and the selected validation profile to the pull-request description:

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
