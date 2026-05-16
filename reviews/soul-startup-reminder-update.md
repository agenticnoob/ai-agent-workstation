# SOUL Startup Reminder Update Review

## What was done

Updated `/Users/ai/.hermes/SOUL.md` to add a `Startup Workflow Reminder` section.

## Behavior added

Hermes should now briefly remind the user at the beginning of fresh sessions, after major context resets, or when starting a new task:

```text
当前工作流：OpenHuman Recall → Hermes planning/review → Codex implementation/testing → Hermes review → OpenHuman Ingestion。
常用方式：告诉我 repo 路径和目标；我先读取 OpenHuman/memory context，写 Codex task；Codex 执行后写 result；我再 review 并提取 memory candidates。
主入口：/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/
```

It also records the practical invocation pattern:

```text
按 codex-hermes-openhuman workflow 执行。开始前读取 OpenHuman/memory context，结束后生成 OpenHuman memory candidates。
```

## Files changed

- `/Users/ai/.hermes/SOUL.md`
- `/Users/ai/agent-workspace/reviews/soul-startup-reminder-update.md`

## Persistent memory

Added a user preference memory that the user wants this workflow reminder at fresh sessions, resets, or new tasks.

## Risk

The reminder could become noisy if repeated too often, so SOUL says to keep it compact and not repeat the full workflow in every reply.

## Verdict

APPROVED
