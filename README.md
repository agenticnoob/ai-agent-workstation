# AI Agent Workspace

English | [中文](README.zh-CN.md)

This is the local AI agent workstation workspace for [Codex](https://openai.com/codex/), [Hermes Agent](https://github.com/NousResearch/hermes-agent), and [OpenHuman](https://github.com/OpenHuman-ai/OpenHuman) collaboration.

Repository name: `ai-agent-workstation`

## Main directories

```text
templates/   Generic reusable templates
tasks/       Codex task handoffs
results/     Codex execution outputs
reviews/     Hermes reviews
memory/      OpenHuman context snapshots and stable memory candidates
workflows/   Reusable multi-agent workflow definitions
```

Project repositories conventionally live outside this workflow workspace under:

```text
/Users/ai/projects
```

## Current primary workflow

The main multi-agent workflow is:

```text
workflows/codex-hermes-openhuman/
```

Use it for Codex + Hermes Agent + OpenHuman collaboration.

## Default agent roles

- OpenHuman: durable memory and stable context recall/ingestion.
- Hermes: planning, coordination, review, context hygiene.
- Codex: repository editing, tests, builds, debugging, result reports.

## Default artifact flow

```text
OPENHUMAN_CONTEXT.md → AGENT_CONTEXT.md → CODEX_TASK.md → AGENT_RESULT.md → AGENT_REVIEW.md → MEMORY_CANDIDATES.md → OPENHUMAN_INGESTION.md
```

## Safety defaults

- Keep work under `/Users/ai/agent-workspace`.
- Keep project repositories under `/Users/ai/projects` unless a task explicitly provides another path.
- Use Markdown handoff files.
- Do not store secrets in memory, OpenHuman packets, or templates.
- Pause before destructive commands or external integrations.
