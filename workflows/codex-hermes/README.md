# Codex + Hermes Workflow

Purpose: define the current local workflow where Hermes plans/reviews and Codex implements/tests.

Audience: the human operator, Hermes, and Codex task runners.

## Start here

- Human quickstart: `QUICKSTART.zh-CN.md`
- Agent runbook: `AGENT_RUNBOOK.md`

Use this invocation pattern:

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。
```

## Canonical flow

```text
Human goal + constraints
  ↓
Hermes context recall + task planning
  ↓
Codex handoff when implementation/deep repo work is needed
  ↓
Codex implementation/testing + result report
  ↓
Hermes review
  ↓
Memory candidates only for stable non-sensitive facts
```

## Required artifact types

| Artifact | Use when | Template |
| --- | --- | --- |
| `AGENT_CONTEXT.md` | a task needs explicit local context | `templates/AGENT_CONTEXT.template.md` |
| `CODEX_TASK.md` or `tasks/*.md` | Codex needs to implement/test/inspect a repo | `templates/CODEX_TASK.template.md` |
| `AGENT_RESULT.md` or `results/*.md` | Codex reports what it did | `templates/AGENT_RESULT.template.md` |
| `AGENT_REVIEW.md` or `reviews/*.md` | Hermes reviews result/diff/validation | `templates/AGENT_REVIEW.template.md` |
| `MEMORY_CANDIDATES.md` or `memory/*.md` | stable facts may be worth durable memory | `templates/MEMORY_CANDIDATES.template.md` |

## Documentation policy

Keep this workflow intentionally small:

- `README.md` is the index and source-of-truth summary.
- `QUICKSTART.zh-CN.md` is the human-facing quickstart.
- `AGENT_RUNBOOK.md` is the agent-facing operating note.
- `templates/` contains only artifact skeletons used by the flow.
- Avoid separate role/architecture/quality-gate documents unless the workflow grows enough to justify them.
