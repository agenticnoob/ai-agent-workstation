# OpenHuman Workflow Upgrade Review

## What was done

Upgraded the Codex + Hermes Agent + OpenHuman workflow so OpenHuman is explicit in both directions:

- Before work: OpenHuman Recall
- After work: OpenHuman Ingestion

## Files changed

- `/Users/ai/agent-workspace/README.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/README.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/ARCHITECTURE.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/WORKFLOW.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/HANDOFF_PROTOCOL.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/RUNBOOK.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/templates/OPENHUMAN_CONTEXT.template.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/templates/OPENHUMAN_INGESTION.template.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/templates/MEMORY_CANDIDATES.template.md`
- `/Users/ai/.hermes/SOUL.md`

## What changed conceptually

Previous model:

```text
Hermes → Codex → Hermes → memory → OpenHuman
```

Updated model:

```text
OpenHuman Recall → Hermes → Codex → Hermes Review → Memory Candidates → OpenHuman Ingestion
```

## New artifacts

- `OPENHUMAN_CONTEXT.md` or `memory/<project>-openh_context.md`
- `MEMORY_CANDIDATES.md` or `memory/<topic>-memory-candidates.md`
- `OPENHUMAN_INGESTION.md`

## Quality impact

This makes OpenHuman visible as a context loop instead of a vague terminal memory sink.

## Risks

- More artifacts can feel heavier for tiny tasks.
- For simple one-off tasks, OpenHuman recall/ingestion can be skipped explicitly.

## Recommended usage

For non-trivial repo work, ask:

```text
按 codex-hermes-openhuman workflow 执行。开始前读取 OpenHuman/memory context，结束后生成 OpenHuman memory candidates。
```

## Verdict

APPROVED
