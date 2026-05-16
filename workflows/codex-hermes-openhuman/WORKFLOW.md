# Workflow

## Default lifecycle

```text
1. OpenHuman Recall
2. Intake
3. Context gathering
4. Plan
5. Handoff
6. Codex Implementation
7. Validation
8. Hermes Review
9. OpenHuman Ingestion
10. Next action
```

## 1. OpenHuman Recall

Before non-trivial work, Hermes checks for durable context from OpenHuman or local memory files.

Look for:
- `/Users/ai/agent-workspace/memory/OPENHUMAN_CONTEXT.md`
- `/Users/ai/agent-workspace/memory/<project>-openh_context.md`
- project-level `AGENT_CONTEXT.md`
- relevant `memory/*.md` files

If no context snapshot exists and the task is likely to recur, create one from `templates/OPENHUMAN_CONTEXT.template.md`.

Recall should include:
- stable user preferences
- stable workstation conventions
- durable project facts
- known do-not-touch boundaries
- non-sensitive assumptions

Recall should not include:
- secrets
- raw logs
- stale task progress
- unapproved private information

## 2. Intake

Hermes captures:
- user goal
- working directory
- target repo
- constraints
- expected deliverable
- risk level
- whether OpenHuman recall is required
- whether OpenHuman ingestion is expected after completion

If the user request is obvious and safe, proceed. Ask only when ambiguity changes the action.

## 3. Context gathering

Hermes checks:
- recalled OpenHuman context snapshot
- existing `AGENT_CONTEXT.md`
- existing task/result/review files
- repo status if a repo is involved
- existing templates or workflow docs

## 4. Plan

For multi-step work, Hermes writes a short plan or task breakdown.

Recommended task size:
- one focused objective
- one repo or subsystem
- one validation path
- no broad unbounded edits

## 5. Handoff

Hermes writes a Codex task file using:
- `templates/CODEX_TASK_TEMPLATE.md`, or
- `workflows/codex-hermes-openhuman/templates/CODEX_TASK.template.md`

Task files should be saved to:

```text
/Users/ai/agent-workspace/tasks/<task-name>.md
```

For active root-level handoff, also use:

```text
/Users/ai/agent-workspace/CODEX_TASK.md
```

## 6. Codex Implementation

Codex runs inside the target git repository when code edits are needed.

Codex should:
- inspect before editing
- follow allowed-file boundaries
- run validation commands
- write `AGENT_RESULT.md` or `results/<task-name>.md`

## 7. Validation

Codex validates with the commands specified by Hermes.

Examples:
- `pnpm test`
- `pnpm build`
- `python -m pytest`
- `npm run lint`
- project-specific smoke test

If validation cannot run, Codex must explain why.

## 8. Hermes Review

Hermes reviews:
- result file
- git diff
- changed files
- validation output
- risks
- next steps
- memory candidates

Review output goes to:

```text
/Users/ai/agent-workspace/reviews/<task-name>.md
```

or root-level:

```text
/Users/ai/agent-workspace/AGENT_REVIEW.md
```

## 9. OpenHuman Ingestion

Hermes extracts only stable candidates:
- durable repo conventions
- stable environment facts
- repeated workflow lessons
- user preferences
- long-term project decisions

Temporary task progress stays in result/review files.

Memory candidate files go to:

```text
/Users/ai/agent-workspace/memory/<topic>-memory-candidates.md
```

Use:

```text
workflows/codex-hermes-openhuman/templates/MEMORY_CANDIDATES.template.md
workflows/codex-hermes-openhuman/templates/OPENHUMAN_INGESTION.template.md
```

Human approval is required before storing personal, project-critical, or potentially sensitive facts in OpenHuman.

## 10. Next action

Hermes recommends one concrete next step:
- approve merge
- create next task
- run deeper review
- approve memory ingestion
- archive completed artifacts

## Workflow variants

### A. Repo inspection only

```text
OpenHuman recall → Hermes writes inspection task → Codex inspects repo without editing → Codex writes result → Hermes reviews → Hermes writes memory candidates
```

### B. Feature implementation

```text
OpenHuman recall → Hermes writes implementation plan → Codex edits/test → Hermes reviews → iterate until quality gate passes → OpenHuman ingestion candidates
```

### C. Debugging

```text
OpenHuman recall → Hermes writes reproduction-focused task → Codex reproduces → Codex finds root cause → Codex writes fix → Hermes reviews → durable debugging lesson candidate if recurring
```

### D. Research + implementation

```text
OpenHuman recall → Hermes gathers references → writes design brief → writes Codex task → Codex implements → Hermes reviews → OpenHuman ingestion candidates
```

### E. Memory update only

```text
Hermes writes MEMORY_CANDIDATES.md → Human approves → OpenHuman/memory stores stable facts
```
