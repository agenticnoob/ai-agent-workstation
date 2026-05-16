# Codex Task

## Goal

Verify the basic AI agent workstation environment.

## Scope

Work only inside:

/Users/ai/agent-workspace

Do not access:

- Other users' home directories
- System directories
- Homebrew system paths
- Private credentials unless explicitly required

## Steps

1. Print the current working directory.
2. Print the current user.
3. Check paths for:
   - node
   - npm
   - pnpm
   - mise
   - hermes
4. Check whether these directories exist:
   - ~/.hermes
   - ~/agent-workspace
   - ~/agent-workspace/tasks
   - ~/agent-workspace/results
   - ~/agent-workspace/reviews
5. Write findings to AGENT_RESULT.md.

## Rules

- Do not use sudo.
- Do not install packages.
- Do not modify files outside this workspace.
- Ask before making destructive changes.
