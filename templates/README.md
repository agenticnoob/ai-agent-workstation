# Templates

This directory contains reusable Markdown templates for local agent workflows.

## Why this exists

The goal of these templates is to keep work artifacts consistent, easy to scan, and easy to reuse across Hermes, Codex, and future agents.

Instead of rewriting the same structure each time, copy the appropriate template and fill it in.

## Templates

### AGENT_REVIEW_TEMPLATE.md

Use this when writing a review, post-task recap, workstation baseline review, or repo review.

Best for:
- summarizing what was done
- listing what worked and what failed
- recording files changed and commands run
- documenting risks, next steps, and memory candidates

Typical output files:
- `/Users/ai/agent-workspace/AGENT_REVIEW.md`
- `/Users/ai/agent-workspace/reviews/<task-name>.md`

### CODEX_TASK_TEMPLATE.md

Use this when preparing a task handoff for Codex.

Best for:
- implementation tasks
- repo inspection tasks
- debugging tasks
- bounded editing tasks
- test-and-report tasks

Typical output files:
- `/Users/ai/agent-workspace/CODEX_TASK.md`
- `/Users/ai/agent-workspace/tasks/<task-name>.md`

## When to use which template

Use `AGENT_REVIEW_TEMPLATE.md` when the goal is to document outcomes, observations, or a review.

Use `CODEX_TASK_TEMPLATE.md` when the goal is to instruct another agent to perform work.

A simple rule:
- Review = write what happened
- Task = write what should happen

## Recommended workflow

1. Copy the relevant template.
2. Fill in the missing sections.
3. Keep the scope narrow and explicit.
4. Save the finished artifact in the current workspace or project-specific folder.
5. If the result is stable and reusable, consider promoting the pattern into a memory note or a more specialized template.

## Writing guidelines

- Keep filenames descriptive.
- Keep tasks bounded and testable.
- List exact paths when possible.
- Include validation steps when work is expected to change files or behavior.
- State "do not touch" boundaries clearly.
- Prefer short, concrete instructions over vague goals.

## Maintenance

If a template proves useful repeatedly, update it instead of creating a one-off variant.

If a template becomes cluttered or stale, simplify it or split out a more specialized version.

## Notes

These templates are intentionally plain Markdown so they can be used by humans and agents without extra tooling.
