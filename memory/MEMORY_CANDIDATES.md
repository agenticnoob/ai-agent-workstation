# Memory Candidates

## Purpose

This file stages stable, non-sensitive workstation and workflow facts before they are promoted into Hermes persistent memory.

Audience: human operator and Hermes.

## Stable Candidates

The dedicated AI agent workstation runs under the macOS user `ai`.

The main workflow workspace is `/Users/ai/agent-workspace`.

When no project path is specified, project repositories conventionally live under `/Users/ai/projects`.

The primary workflow path is `/Users/ai/agent-workspace/workflows/codex-hermes`.

The preferred workflow is Local context recall → Hermes planning/review → Codex implementation/testing → Hermes review → Hermes memory hygiene.

Hermes acts as planner, context gatherer, Codex task author, reviewer, and memory-candidate curator.

Codex CLI acts as implementation, test execution, build/debug, and result-report agent.

The preferred agent handoff interface is explicit Markdown files, not hidden automatic coupling.

The local `my-agents-mcp` project provides the optional tool layer for the `codex-hermes` workflow: workflow guide lookup, artifact templates/skeletons, `validate_artifact` v0.2 quality-gate checks, and memory candidate guidance.

`my-agents-mcp` is not a workflow source of truth and should not become hidden automation; SOUL.md and `/Users/ai/agent-workspace/workflows/codex-hermes/README.md` plus `AGENT_RUNBOOK.md` remain the primary workflow references.

When `my-agents-mcp` is available, the `codex-hermes` workflow prefers MCP-generated skeletons/templates for new artifacts; files under `/Users/ai/agent-workspace/workflows/codex-hermes/templates/` remain human-readable fallback templates and audit references, not executable handoffs as-is.

Stable facts may be promoted to Hermes persistent memory only when they are non-sensitive, declarative, useful across sessions, and unlikely to become stale within a week.

## Rejected Items

Secrets, token values, API keys, cookies, private keys, `.env` contents, raw logs, one-off task progress, issue/PR status, and commit hashes do not belong in memory candidates.

## Rationale

These candidates describe stable workstation architecture and workflow conventions. They are non-sensitive, declarative, and useful across sessions.

## Review Notes

Promote only candidates that remain accurate after checking SOUL.md and the active `codex-hermes` workflow source-of-truth files.
