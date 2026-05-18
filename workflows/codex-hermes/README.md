# Codex + Hermes Workflow

Purpose: provide an inspectable local workflow where Hermes plans/reviews and Codex implements/tests.

Audience: the human operator, Hermes, and Codex task runners.

## Roles

- Human/User: goals, constraints, risk tolerance, credentials, and final approval.
- Hermes Agent: context gathering, planning, Markdown handoffs, Codex task preparation, review, and memory hygiene.
- Codex CLI: repository inspection, edits, tests, builds, debugging, and result reporting.

## Default flow

```text
Local context recall
  ↓
Hermes planning/review
  ↓
Codex implementation/testing
  ↓
Codex result report
  ↓
Hermes review
  ↓
Hermes memory candidates when useful
```

## Invocation pattern

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。
```

## Quickstart

- Chinese quickstart: `QUICKSTART.zh-CN.md`

## Key files

- `AGENT_CONTEXT.md` — task-local context for agents.
- `CODEX_TASK.md` or `tasks/*.md` — bounded Codex handoff.
- `AGENT_RESULT.md` or `results/*.md` — Codex result report.
- `AGENT_REVIEW.md` or `reviews/*.md` — Hermes review.
- `MEMORY_CANDIDATES.md` or `memory/*.md` — stable non-sensitive facts worth considering for Hermes memory.
