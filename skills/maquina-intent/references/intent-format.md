# Intent format

Prefer `maquina intent create` when the repository supplies it. It creates the
JSON safely and requires at least one allowed path, context reference, and
acceptance criterion:

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

When the command is unavailable, create JSON with this minimum shape:

```json
{
  "schema_version": "maquina.intent.v1",
  "id": "TEAM-123",
  "title": "Short outcome-oriented title",
  "objective": "What will change and why.",
  "work_type": "backend",
  "allowed_paths": ["service/handler.go", "service/handler_test.go"],
  "context_refs": ["AGENTS.md", "docs/architecture.md"],
  "acceptance_criteria": ["A specific observable outcome."]
}
```

Use a work type permitted by the Factory Contract. `allowed_paths` may name a file or directory prefix. Keep criteria testable and avoid invented metrics.
