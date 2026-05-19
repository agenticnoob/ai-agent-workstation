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
MCP-assisted artifact templates + validate_artifact v0.2 quality checks when available
  ↓
Codex handoff when implementation/deep repo work is needed
  ↓
Codex implementation/testing + result report
  ↓
Hermes review + artifact validation
  ↓
Memory candidates only for stable non-sensitive facts
```

## MCP helper layer

The local `my-agents-mcp` server is the optional tool layer for this workflow. It provides:

- workflow guide lookup
- Markdown artifact templates and skeletons
- `validate_artifact` v0.2 quality-gate validation
- memory candidate guidance

The MCP server does not replace this Markdown workflow, SOUL.md, or human approval. It must not auto-run Codex, auto-write persistent memory, auto-commit git changes, or modify Hermes configuration.

Governance sync rule: SOUL.md, `/Users/ai/agent-workspace` workflow docs, and `/Users/ai/projects/my-agents-mcp` are a strongly linked set. When any one changes, check whether the other two need corresponding updates and record that decision in the review or final response.

Use `validate_artifact` before key gates:

- Gate 0: validate `CODEX_TASK.md` before Codex starts.
- Gate 1/2: validate `AGENT_RESULT.md` before review.
- Gate 3: validate `AGENT_REVIEW.md` before final response.
- Gate 4: validate `MEMORY_CANDIDATES.md` before memory promotion.

v0.2 validation checks required sections plus quality issues: empty sections, placeholder text, weak Codex handoffs, invalid review verdicts, missing validation notes, unsafe memory candidates, and stale memory candidates.

## Required artifact types

When `my-agents-mcp` is available, prefer MCP-generated skeletons/templates (`create_codex_task_skeleton` or `get_artifact_template`) and then validate the filled artifact with `validate_artifact` v0.2. The files under `templates/` remain the human-readable fallback templates and audit references; they contain placeholders and are not expected to pass validation as executable artifacts until copied and filled.

| Artifact | Use when | Template |
| --- | --- | --- |
| `AGENT_CONTEXT.md` | a task needs explicit local context | `templates/AGENT_CONTEXT.template.md` |
| `CODEX_TASK.md` or `tasks/*.md` | Codex needs to implement/test/inspect a repo | `templates/CODEX_TASK.template.md` |
| `AGENT_RESULT.md` or `results/*.md` | Codex reports what it did | `templates/AGENT_RESULT.template.md` |
| `AGENT_REVIEW.md` or `reviews/*.md` | Hermes reviews result/diff/validation | `templates/AGENT_REVIEW.template.md` |
| `MEMORY_CANDIDATES.md` or `memory/*.md` | stable facts may be worth durable memory | `templates/MEMORY_CANDIDATES.template.md` |

## Codex invocation note

For Codex CLI handoffs, prefer the current sandbox flag:

```bash
codex exec --sandbox workspace-write 'Read CODEX_TASK.md and complete it exactly. Keep terminal output concise; write durable details to AGENT_RESULT.md.'
```

Avoid the deprecated `--full-auto` flag in new handoffs.

## Documentation policy

Keep this workflow intentionally small:

- `README.md` is the index and source-of-truth summary.
- `QUICKSTART.zh-CN.md` is the human-facing quickstart.
- `AGENT_RUNBOOK.md` is the agent-facing operating note.
- `templates/` contains only artifact skeletons used by the flow.
- Avoid separate role/architecture/quality-gate documents unless the workflow grows enough to justify them.
