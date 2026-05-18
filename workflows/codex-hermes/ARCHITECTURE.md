# Architecture

```text
Human/User
  ↓ goals, constraints, approval
Hermes Agent
  ↓ plans, task files, reviews, context hygiene
Codex CLI
  ↓ repository edits, tests, builds, debugging, result reports
Hermes Agent
  ↑ review, memory candidates, next step
```

The integration boundary is Markdown handoff files, not hidden automatic coupling.
