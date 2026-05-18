# Runbook

## Start a repo task

```text
按 codex-hermes workflow 执行。Repo: /Users/ai/projects/<repo>. Goal: <goal>. Constraints: <constraints>.
```

## Create a Codex task

Use `templates/CODEX_TASK.template.md` and write the task under `tasks/` or the repo root as `CODEX_TASK.md`.

## Review Codex result

Read the result file, inspect changed files and git diff, check validation output, then write a review under `reviews/` or `AGENT_REVIEW.md`.

## Memory candidates

Only write memory candidates for durable non-sensitive facts that will still matter across sessions.
