# OpenHuman Memory Candidates

## Purpose

This file stages stable, non-sensitive workstation and workflow facts before they are promoted into OpenHuman or another durable memory backend.

Audience: human operator, Hermes, and OpenHuman ingestion tooling.

Status: version 3 selected by user for OpenHuman ingestion packet
Date: 2026-05-17
Prepared by: Hermes

## Source artifacts

- Active policy: `/Users/ai/.hermes/SOUL.md`
- Workflow directory: `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/`
- Review artifact: `/Users/ai/agent-workspace/reviews/soul-startup-reminder-update.md`
- Existing memory README: `/Users/ai/agent-workspace/memory/README.md`

## Candidate facts

### Candidate 1

- Fact: The dedicated AI agent workstation runs under the macOS user `ai`.
- Why durable: This is a stable workstation identity and isolation boundary.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 2

- Fact: The main workspace is `/Users/ai/agent-workspace`.
- Why durable: This is the default location for local agent workflow artifacts.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 3

- Fact: When no project path is specified, project repositories conventionally live under `/Users/ai/projects`.
- Why durable: This is a stable workstation organization convention.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 4

- Fact: The primary workflow path is `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman`.
- Why durable: This is the main reusable workflow definition for the workstation.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 5

- Fact: The preferred workflow is OpenHuman Recall → Hermes planning/review → Codex implementation/testing → Hermes review → OpenHuman Ingestion.
- Why durable: This defines the workstation's intended multi-agent operating model.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 6

- Fact: Hermes acts as planner, context gatherer, Codex task author, reviewer, and memory-candidate curator.
- Why durable: This is a stable role boundary in the local workflow.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 7

- Fact: Codex CLI acts as implementation, test execution, build/debug, and result-report agent.
- Why durable: This is a stable role boundary in the local workflow.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 8

- Fact: OpenHuman is treated as the durable context and memory layer for stable, non-sensitive facts.
- Why durable: This establishes the boundary between temporary task artifacts and long-term context.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

### Candidate 9

- Fact: Markdown handoff files are the preferred coordination interface between Hermes, Codex, OpenHuman, and the human operator.
- Why durable: This is a recurring workflow convention and keeps automation inspectable.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: deferred; keep in workflow docs for now

### Candidate 10

- Fact: Standard workflow artifacts include `AGENT_CONTEXT.md`, `CODEX_TASK.md`, `AGENT_RESULT.md`, `AGENT_REVIEW.md`, `MEMORY_CANDIDATES.md`, and `OPENHUMAN_INGESTION.md`, with reusable variants under `tasks/`, `results/`, `reviews/`, and `memory/`.
- Why durable: These artifact names define the local handoff convention.
- Scope: workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: deferred; keep in workflow docs for now

### Candidate 11

- Fact: At fresh sessions, major context resets, or new tasks, the user wants a compact reminder of the active Codex + Hermes Agent + OpenHuman workflow and practical invocation pattern.
- Why durable: This is a stable user preference that improves future task intake.
- Scope: user
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman and Hermes user memory
- Approval status: selected for ingestion packet

### Candidate 12

- Fact: A practical invocation pattern is: `按 codex-hermes-openhuman workflow 执行。开始前读取 OpenHuman/memory context，结束后生成 OpenHuman memory candidates。`
- Why durable: This is a reusable command phrase for triggering the intended workflow.
- Scope: user / workstation
- Sensitivity check: non-sensitive
- Recommended destination: OpenHuman
- Approval status: selected for ingestion packet

## Rejected candidates

- No secrets, token values, raw command outputs, one-off task progress, PR numbers, issue numbers, or commit hashes were included.

## OpenHuman ingestion recommendation

- Create ingestion packet: yes; version 3 selected by user.
- Suggested file: `/Users/ai/agent-workspace/memory/OPENHUMAN_INGESTION.md`
- Created file: `/Users/ai/agent-workspace/memory/OPENHUMAN_INGESTION.md`

## Human approval

- Approved by: user selected version 3
- Date: 2026-05-17
