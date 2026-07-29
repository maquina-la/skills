# Intent format

Create JSON with this minimum shape:

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
