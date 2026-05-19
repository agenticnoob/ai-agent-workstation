# Codex + Hermes Workflow

Purpose: source-of-truth summary for the local Hermes + Codex workflow.
Audience: the human operator, Hermes, and Codex task runners.

## One-line use

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。
```

## Active docs

- `QUICKSTART.zh-CN.md` — human-facing quickstart
- `AGENT_RUNBOOK.md` — agent-facing operating note
- `templates/` — only the skeletons actually used by the flow

## Default flow

```text
Human goal + constraints
  ↓
Hermes context recall + bounded task
  ↓
Codex handoff when implementation / debugging / test runs are needed
  ↓
Codex result report
  ↓
Hermes review + memory hygiene
```

## Keep the workflow small

- Keep tasks bounded: working directory, allowed files, do-not-touch, validation, result path.
- Use direct Hermes action for simple inspection or documentation work.
- Use Codex for repo edits, build/test/debug loops, or broader inspection.
- Keep only stable, non-sensitive facts in memory candidates.
- Use `my-agents-mcp` as an optional helper for guide lookup, templates, and `validate_artifact` v0.2.
- MCP does not replace `SOUL.md` or these Markdown docs.

## Governance sync

`SOUL.md`, `/Users/ai/agent-workspace` workflow docs, and `/Users/ai/projects/my-agents-mcp` are a strongly linked set. When one changes, check whether the other two need corresponding updates.
