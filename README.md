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

## Default agent roles

- Hermes: planning, coordination, review, context hygiene, and memory hygiene.
- Codex: repository editing, tests, builds, debugging, and result reports.
- Human/User: product direction, constraints, approvals, credentials, and final decisions.

## Default artifact flow

```text
AGENT_CONTEXT.md → CODEX_TASK.md → AGENT_RESULT.md → AGENT_REVIEW.md → MEMORY_CANDIDATES.md
```

## Safety defaults

- Keep workflow artifacts under `/Users/ai/agent-workspace`.
- Keep project repositories under `/Users/ai/projects` unless a task explicitly provides another path.
- Use Markdown handoff files.
- Do not store secrets in memory candidates, templates, task files, result files, or review files.
- Pause before destructive commands or external integrations.
