# OpenHuman Ingestion Packet

## Scope

- Destination: workstation / user
- Project or repo: local AI agent workstation
- Prepared by: Hermes
- Approval status: selected by user from `OPENHUMAN_CANDIDATES.md` version 3
- Date: 2026-05-17

## Source artifacts

- Active policy: `/Users/ai/.hermes/SOUL.md`
- Workflow directory: `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/`
- Memory candidates: `/Users/ai/agent-workspace/memory/OPENHUMAN_CANDIDATES.md`
- Review artifact: `/Users/ai/agent-workspace/reviews/soul-startup-reminder-update.md`

## Approved facts to ingest

### Fact 1

- Fact: The dedicated AI agent workstation runs under the macOS user `ai`.
- Why durable: This is a stable workstation identity and isolation boundary.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 2

- Fact: The main workspace is `/Users/ai/agent-workspace`.
- Why durable: This is the default location for local agent workflow artifacts.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 3

- Fact: When no project path is specified, project repositories conventionally live under `/Users/ai/projects`.
- Why durable: This is a stable workstation organization convention.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 4

- Fact: The primary workflow path is `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman`.
- Why durable: This is the main reusable workflow definition for the workstation.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 5

- Fact: The preferred workflow is OpenHuman Recall → Hermes planning/review → Codex implementation/testing → Hermes review → OpenHuman Ingestion.
- Why durable: This defines the workstation's intended multi-agent operating model.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 6

- Fact: Hermes acts as planner, context gatherer, Codex task author, reviewer, and memory-candidate curator.
- Why durable: This is a stable role boundary in the local workflow.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 7

- Fact: Codex CLI acts as implementation, test execution, build/debug, and result-report agent.
- Why durable: This is a stable role boundary in the local workflow.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 8

- Fact: OpenHuman is treated as the durable context and memory layer for stable, non-sensitive facts.
- Why durable: This establishes the boundary between temporary task artifacts and long-term context.
- Sensitivity check: non-sensitive
- Destination scope: workstation

### Fact 9

- Fact: At fresh sessions, major context resets, or new tasks, the user wants a compact reminder of the active Codex + Hermes Agent + OpenHuman workflow and practical invocation pattern.
- Why durable: This is a stable user preference that improves future task intake.
- Sensitivity check: non-sensitive
- Destination scope: user

### Fact 10

- Fact: A practical invocation pattern is: `按 codex-hermes-openhuman workflow 执行。开始前读取 OpenHuman/memory context，结束后生成 OpenHuman memory candidates。`
- Why durable: This is a reusable command phrase for triggering the intended workflow.
- Sensitivity check: non-sensitive
- Destination scope: user / workstation

## Rejected or deferred facts

- Deferred: Markdown handoff files are the preferred coordination interface between Hermes, Codex, OpenHuman, and the human operator.
- Deferred: Standard workflow artifacts include `AGENT_CONTEXT.md`, `CODEX_TASK.md`, `AGENT_RESULT.md`, `AGENT_REVIEW.md`, `MEMORY_CANDIDATES.md`, and `OPENHUMAN_INGESTION.md`, with reusable variants under `tasks/`, `results/`, `reviews/`, and `memory/`.

Reason: these two facts are useful workflow details, but they are more implementation-specific and can remain in workflow documentation instead of being promoted into compact long-term memory.

## Notes

- Do not ingest secrets, token values, one-off task progress, PR/issue status, commit hashes, or raw logs.
- Facts are written declaratively rather than as imperative instructions.
- This file is an ingestion packet/staging artifact. It does not by itself prove that OpenHuman has already imported the facts.
