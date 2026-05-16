# Architecture

## System roles

```text
┌────────────┐
│ OpenHuman  │
└─────┬──────┘
      │ Recall: stable user/project/workstation context
      ▼
┌────────────┐
│   Human    │
└─────┬──────┘
      │ goals, constraints, approval
      ▼
┌────────────┐
│  Hermes    │  planning, coordination, review, context hygiene
└─────┬──────┘
      │ Markdown handoff files
      ▼
┌────────────┐
│   Codex    │  repo edits, tests, builds, debugging
└─────┬──────┘
      │ AGENT_RESULT.md / results/*.md
      ▼
┌────────────┐
│  Hermes    │  review, risk analysis, next task, memory candidates
└─────┬──────┘
      │ Ingestion: approved durable facts only
      ▼
┌────────────┐
│ OpenHuman  │
└────────────┘
```

## Design principles

1. OpenHuman as context loop
   - Before work, recall durable context.
   - After work, ingest only approved stable facts.
   - OpenHuman is not the code executor and not the task tracker.

2. File-first coordination
   - Every non-trivial task gets a task file.
   - Every implementation run gets a result file.
   - Every review gets a review file.
   - Every memory update gets a candidate file before ingestion.

3. Role separation
   - Hermes does planning and review.
   - Codex does implementation and test execution.
   - OpenHuman stores durable context.

4. Human checkpoints
   - Human approval is required for risky operations, external integrations, credentials, destructive commands, ambiguous product decisions, and memory ingestion containing personal or sensitive context.

5. Small reversible steps
   - Prefer small task files and frequent validation.
   - Avoid broad prompts like "improve this repo".

6. Memory hygiene
   - Stable conventions can become memory.
   - Temporary task status should stay in results/reviews, not OpenHuman.

## State boundaries

| State type | Owner | Location |
|---|---|---|
| Recalled durable context | OpenHuman → Hermes | `memory/OPENHUMAN_CONTEXT.md`, `memory/<project>-openh_context.md` |
| Current task context | Hermes | `AGENT_CONTEXT.md`, `tasks/*.md` |
| Implementation details | Codex | repo files, `AGENT_RESULT.md`, `results/*.md` |
| Review and risk notes | Hermes | `AGENT_REVIEW.md`, `reviews/*.md` |
| Memory candidates | Hermes drafts, Human approves | `memory/*-memory-candidates.md` |
| Durable facts | OpenHuman / memory layer | OpenHuman store after approval |
| Templates | Hermes | `templates/*.md`, `workflows/*/templates/*.md` |

## Recommended agent interaction

### Simple task

```text
Human → Hermes → local file edit/review → final answer
```

### Repo implementation task

```text
OpenHuman recall → Hermes writes CODEX_TASK.md → Codex executes → Codex writes AGENT_RESULT.md → Hermes reviews → Hermes writes memory candidates → Human approves OpenHuman ingestion
```

### Long-running multi-step project

```text
OpenHuman context snapshot → Hermes creates plan + tasks/ → Codex executes task by task → Hermes reviews each result → OpenHuman ingests approved stable facts
```
