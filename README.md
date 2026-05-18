# AI Agent Workspace

English | [中文](README.zh-CN.md)

This is the local AI agent workstation workspace for [Hermes Agent](https://github.com/NousResearch/hermes-agent) and [Codex](https://openai.com/codex/) collaboration.

Repository name: `ai-agent-workstation`

## Main directories

```text
templates/   Generic reusable templates
tasks/       Codex task handoffs
results/     Codex execution outputs
reviews/     Hermes reviews
memory/      Local memory candidates and durable workstation notes
workflows/   Reusable multi-agent workflow definitions
```

Project repositories conventionally live outside this workflow workspace under:

```text
/Users/ai/projects
```

## Current primary workflow

The main multi-agent workflow is:

```text
workflows/codex-hermes/
```

Use it for Hermes planning/review plus Codex implementation/testing.

Quickstart:

```text
workflows/codex-hermes/QUICKSTART.zh-CN.md
```

## Default agent roles

- Hermes: planning, coordination, review, context hygiene, and memory hygiene.
- Codex: repository editing, tests, builds, debugging, and result reports.
- Human/User: product direction, constraints, approvals, credentials, and final decisions.

## Default artifact flow

```text
AGENT_CONTEXT.md → CODEX_TASK.md → AGENT_RESULT.md → AGENT_REVIEW.md → MEMORY_CANDIDATES.md
```

When `my-agents-mcp` is available, use it as the workflow helper layer for artifact templates and `validate_artifact` v0.2 quality-gate validation. It does not replace the Markdown workflow docs or SOUL.md, and it must not become hidden automation.

Governance sync rule: SOUL.md, this workspace documentation, and `/Users/ai/projects/my-agents-mcp` are a strongly linked set. When changing any one of them, check whether the other two need corresponding updates and record the decision in the review or final response.

Typical MCP-assisted gates:

- Validate `CODEX_TASK.md` before Codex starts.
- Validate `AGENT_RESULT.md` before Hermes review.
- Validate `AGENT_REVIEW.md` before final response.
- Validate `MEMORY_CANDIDATES.md` before memory promotion.

## Safety defaults

- Keep workflow artifacts under `/Users/ai/agent-workspace`.
- Keep project repositories under `/Users/ai/projects` unless a task explicitly provides another path.
- Use Markdown handoff files.
- Do not store secrets in memory candidates, templates, task files, result files, or review files.
- Pause before destructive commands or external integrations.
