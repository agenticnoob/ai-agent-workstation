# Example: Repo Inspection Workflow

## User asks

```text
Inspect /Users/ai/projects/example-app and prepare it for Codex work.
```

## Hermes creates task

File:

```text
/Users/ai/agent-workspace/tasks/inspect-example-app.md
```

Task summary:
- identify package manager
- identify test/build/lint commands
- list repo structure
- do not modify source files
- write result to `results/inspect-example-app.md`

## Codex executes

Inside repo:

```bash
codex exec "Read /Users/ai/agent-workspace/tasks/inspect-example-app.md and complete it."
```

## Codex writes result

```text
/Users/ai/agent-workspace/results/inspect-example-app.md
```

## Hermes reviews

Hermes checks:
- result content
- git status
- whether source files changed unexpectedly
- whether commands are plausible

Hermes writes:

```text
/Users/ai/agent-workspace/reviews/inspect-example-app.md
```

## Memory candidates

Only stable findings are proposed, for example:

```text
Project example-app uses pnpm and Vitest. Test command is pnpm test.
```

Do not store:

```text
Codex finished inspection today.
```
