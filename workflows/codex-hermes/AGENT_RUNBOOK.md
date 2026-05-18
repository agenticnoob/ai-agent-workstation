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

4. Use artifacts and MCP helpers when available.
   - If `my-agents-mcp` is available, prefer its skeleton/template helpers (`create_codex_task_skeleton` or `get_artifact_template`) and `validate_artifact` v0.2 instead of relying only on hand-written structure.
   - Keep `templates/*.template.md` as human-readable fallback templates and audit references. They contain placeholders and should not be handed to Codex as-is.
   - Context: fill `AGENT_CONTEXT.md` from `templates/AGENT_CONTEXT.template.md` or the MCP template output.
   - Codex handoff: fill `CODEX_TASK.md` or `tasks/<task-name>.md` from `create_codex_task_skeleton`, `get_artifact_template`, or `templates/CODEX_TASK.template.md`.
   - Codex result: expect `AGENT_RESULT.md` or `results/<task-name>.md`.
   - Hermes review: write `AGENT_REVIEW.md` or `reviews/<task-name>.md`.
   - Memory candidates: write `MEMORY_CANDIDATES.md` or `memory/<topic>.md`.

5. Validate artifacts at workflow gates.
   - Before Codex starts, validate `CODEX_TASK.md`; it must have concrete scope, boundaries, validation commands or explicit Codex discovery policy, and result path.
   - After Codex finishes, validate `AGENT_RESULT.md` for required report sections.
   - Before final review, validate `AGENT_REVIEW.md`; verdict must be exactly `APPROVED`, `NEEDS_CHANGES`, or `BLOCKED`, and validation checked must describe what actually ran or why it could not run.
   - Before memory promotion, validate `MEMORY_CANDIDATES.md`; stable candidates must not contain secrets, credentials, token values, commit hashes, issue/PR status, build IDs, or one-off progress wording. Rejected-item sections may name excluded categories as exclusions.

6. Review before final response.
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
