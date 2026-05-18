# Memory Candidates

## Purpose

This file stages stable, non-sensitive workstation and workflow facts before they are promoted into Hermes persistent memory.

Audience: human operator and Hermes.

## Current stable facts

The dedicated AI agent workstation runs under the macOS user `ai`.

The main workflow workspace is `/Users/ai/agent-workspace`.

When no project path is specified, project repositories conventionally live under `/Users/ai/projects`.

The primary workflow path is `/Users/ai/agent-workspace/workflows/codex-hermes`.

The preferred workflow is Local context recall → Hermes planning/review → Codex implementation/testing → Hermes review → Hermes memory hygiene.

Hermes acts as planner, context gatherer, Codex task author, reviewer, and memory-candidate curator.

Codex CLI acts as implementation, test execution, build/debug, and result-report agent.

The preferred agent handoff interface is explicit Markdown files, not hidden automatic coupling.

Stable facts may be promoted to Hermes persistent memory only when they are non-sensitive, declarative, useful across sessions, and unlikely to become stale within a week.

## Excluded facts

Secrets, token values, API keys, cookies, private keys, `.env` contents, raw logs, one-off task progress, issue/PR status, and commit hashes do not belong in memory candidates.
