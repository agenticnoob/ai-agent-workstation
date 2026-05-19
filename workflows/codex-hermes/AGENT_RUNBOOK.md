# Agent Runbook: Codex + Hermes Workflow

Purpose: short operating note for Hermes and Codex task runners.
Audience: Hermes Agent and Codex task runners.

## Rule

`QUICKSTART.zh-CN.md` is human-facing. Use this file and the templates in `templates/` for execution.

## Default sequence

1. Recall only the context that matters.
2. Bound the task:
   - working directory
   - allowed files
   - do-not-touch paths
   - validation commands
   - result file path
3. Pick the path:
   - simple safe inspection or documentation task → Hermes acts directly
   - repo implementation, debugging, build/test loops → write a Codex task first
4. If `my-agents-mcp` is available, prefer its skeleton/template helpers and `validate_artifact` v0.2.
5. Review result, diff, and validation before final reply.

## Codex task minimum fields

Goal
Context
Working Directory
Allowed Files
Do Not Touch
Steps
Validation
Expected Output
Result File
Safety Notes

## Memory filter

Keep only stable, non-sensitive, reusable facts.

Do not save:

- temporary task progress
- issue / PR / commit status
- one-off logs
- secrets or `.env` content
- facts likely to expire within a week

## Keep docs small

Update `README.md`, `AGENT_RUNBOOK.md`, `QUICKSTART.zh-CN.md`, and `templates/` instead of reintroducing many parallel docs.
