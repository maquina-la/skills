---
name: maquina-pr-advisory
description: Prepare and interpret a Máquina pull-request operational advisory without treating it as code review or merge approval. Use when opening, updating, or investigating a PR governed by a Máquina Factory Contract, including missing intent metadata, validation evidence, protected-resource handling, or advisory comments.
---

# Máquina PR advisory

Use the pull request as the control point. Máquina evaluates declared context, validation evidence, policy conditions, and required human handling. It does not judge code quality or approve a merge.

## Prepare the pull request

1. Read `.maquina/factory-contract.json` and the linked intent.
2. Confirm every changed path is within the intent's `allowed_paths`.
3. Run the validation profile declared by the PR and retain only its outcome as evidence.
4. Add or preserve the three metadata lines in [PR metadata](references/pr-metadata.md).
5. Ensure the workflow evaluates the Factory Contract from the trusted base revision, not from untrusted PR content.
6. Keep GitHub token permissions read-only unless the repository has explicitly enabled same-repository operational-comment projection.

## Interpret the result

- `ready_for_human_review` means the observed conditions are satisfied; it is not merge approval.
- `needs_attention` means a declared condition is absent or failed. Resolve the named condition, then rerun.
- A missing intent is a planning gap. Create a narrowly scoped intent on the trusted base branch, then link the PR.
- A protected-path observation is a request for the contract's defined human handling, not an automatic rejection.

## Safety

- Do not convert the advisory into a required merge gate without an explicit policy decision.
- Never publish code, diffs, prompts, secrets, raw model outputs, or verbose traces in shared evidence or comments.
- Suppress comment publication for fork pull requests.
