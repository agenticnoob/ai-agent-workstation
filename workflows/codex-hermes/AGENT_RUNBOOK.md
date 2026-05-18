# Agent Runbook: Codex + Hermes Workflow

Purpose: give Hermes and Codex task runners a short operating note for executing the local workflow without rereading the human quickstart.

Audience: Hermes Agent and Codex task runners.

## Operating rule

Do not treat `QUICKSTART.zh-CN.md` as agent instructions. It is a human-facing quickstart.

Use this file plus the templates in `templates/` when executing the workflow.

## Default sequence

1. Recall context.
   - Check relevant Hermes memory already in session.
   - Read local memory notes only when relevant.
   - Inspect prior task/result/review artifacts only when they affect the task.

2. Bound the task.
   - Confirm working directory.
   - Define allowed files and do-not-touch paths.
   - Define validation commands.
   - Define result/review file paths.

3. Choose execution path.
   - Simple safe documentation or inspection task: Hermes may act directly.
   - Repo implementation, debugging, broad inspection, or test/build loop: write a Codex task first.

4. Use artifacts.
   - Context: `AGENT_CONTEXT.md` or `templates/AGENT_CONTEXT.template.md`.
   - Codex handoff: `CODEX_TASK.md` or `templates/CODEX_TASK.template.md`.
   - Codex result: `AGENT_RESULT.md` or `templates/AGENT_RESULT.template.md`.
   - Hermes review: `AGENT_REVIEW.md` or `templates/AGENT_REVIEW.template.md`.
   - Memory candidates: `MEMORY_CANDIDATES.md` or `templates/MEMORY_CANDIDATES.template.md`.

5. Review before final response.
   - Read result file if Codex wrote one.
   - Check changed files and git diff when files changed.
   - Check validation output or state why validation was not run.
   - Mark verdict: `APPROVED`, `NEEDS_CHANGES`, or `BLOCKED`.

## Codex task minimum fields

- Goal
- Context
- Working Directory
- Allowed Files
- Do Not Touch
- Steps
- Validation
- Expected Output
- Result File
- Safety Notes

## Memory filter

Save only stable, non-sensitive, reusable facts.

Do not save:

- temporary task progress
- issue / PR / commit status
- one-off logs
- secrets or `.env` content
- facts likely to expire within a week

## Keep docs small

If workflow docs drift, prefer updating:

- `README.md` for source-of-truth summary
- `AGENT_RUNBOOK.md` for agent execution notes
- `QUICKSTART.zh-CN.md` for human-facing usage

Do not recreate separate architecture, roles, workflow, handoff, runbook, or quality gate files unless the user explicitly asks for a larger documentation set.
