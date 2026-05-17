# OpenHuman Memory: AI Agent Workstation

This document is written for OpenHuman ingestion. It contains stable, non-sensitive facts that should help future agents understand the local AI engineering workstation without importing temporary task state.

## Workstation Identity

The workstation is a dedicated local AI agent environment running under the macOS user `ai`.

The main workflow workspace is `/Users/ai/agent-workspace`.

When no project path is specified, project repositories conventionally live under `/Users/ai/projects`.

The primary reusable workflow is stored at `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman`.

## Operating Model

The preferred workstation workflow is:

```text
OpenHuman Recall → Hermes planning/review → Codex implementation/testing → Hermes review → OpenHuman Ingestion
```

OpenHuman is the durable context and memory layer. It should store stable, non-sensitive facts that are useful across sessions.

Hermes Agent is the planner, context gatherer, Codex task author, reviewer, and memory-candidate curator.

Codex CLI is the implementation and validation agent. It handles repository inspection, source edits, tests, builds, debugging, and result reports.

The human operator owns goals, constraints, final approval, risk tolerance, credentials, and external integrations.

## User Preference

The user prefers a compact workflow reminder at the start of fresh sessions, after major context resets, or when beginning a new task.

The reminder should mention the active Codex + Hermes Agent + OpenHuman workflow and the practical invocation pattern, but it should not be repeated in every response.

A useful invocation pattern is:

```text
按 codex-hermes-openhuman workflow 执行。开始前读取 OpenHuman/memory context，结束后生成 OpenHuman memory candidates。
```

## Memory Boundaries

OpenHuman memory should contain durable facts, not task logs.

Do not ingest secrets, token values, API keys, cookies, private keys, `.env` contents, raw logs, one-off task progress, PR status, issue status, or commit hashes.

Facts should be declarative rather than imperative. Procedures and reusable workflows should live in workflow documentation or skills, not as long-term memory facts.

## Source

This memory was prepared from the local workstation policy and the selected version 3 memory candidates in `/Users/ai/agent-workspace/memory/OPENHUMAN_CANDIDATES.md`.
