# Agent Workstation Context

## Machine

This is a dedicated macOS user environment for AI agent work.

User:

- macOS user: ai
- Home directory: /Users/ai
- Main workspace: /Users/ai/agent-workspace

## Agent Roles

- Hermes: planning, task management, review, long-term project coordination, and memory hygiene
- Codex: code reading, code editing, tests, builds, repo-level execution, and result reporting

## Safety Boundaries

Agents must:

- Work only under /Users/ai unless explicitly instructed otherwise
- Prefer /Users/ai/agent-workspace for workflow artifacts
- Prefer /Users/ai/projects for project repositories
- Avoid accessing the main user's home directory
- Avoid using sudo
- Avoid changing system-level files
- Avoid modifying Homebrew directories
- Avoid enabling gateway, messaging, cron, or external integrations without explicit approval

## Current Policy

- Hermes runs locally.
- Codex should be run inside tmux for long tasks.
- Handoff between agents should happen through Markdown files.
- External services such as Gmail, Drive, Calendar, Telegram, Discord, and gateway are disabled for now.

## Standard Handoff Files

- AGENT_CONTEXT.md: stable workstation/project context
- CODEX_TASK.md: task given to Codex
- AGENT_RESULT.md: result produced by Codex
- AGENT_REVIEW.md: review and next-step analysis by Hermes or human
- MEMORY_CANDIDATES.md: durable non-sensitive facts to consider for Hermes persistent memory
