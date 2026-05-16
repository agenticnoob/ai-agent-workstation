# Runbook

## Start a new project workflow

1. Put the repo under:

```text
/Users/ai/projects/<repo-name>
```

2. Recall OpenHuman context.

Check for:

```text
/Users/ai/agent-workspace/memory/OPENHUMAN_CONTEXT.md
/Users/ai/agent-workspace/memory/<repo-name>-openh_context.md
```

If missing and the repo will be reused, create a context snapshot from:

```text
workflows/codex-hermes-openhuman/templates/OPENHUMAN_CONTEXT.template.md
```

3. Ask Hermes to inspect the repo and create context:

```text
Inspect this repo, use OpenHuman/memory context if available, identify package manager, test commands, build commands, and write AGENT_CONTEXT.md.
```

4. Hermes creates:

```text
AGENT_CONTEXT.md
tasks/inspect-<repo>.md
```

5. Codex executes the inspection task and writes:

```text
results/inspect-<repo>.md
```

6. Hermes reviews and writes:

```text
reviews/inspect-<repo>.md
```

7. Hermes extracts stable memory candidates:

```text
memory/<repo>-memory-candidates.md
```

8. Human approves selected candidates for OpenHuman ingestion.

## Create a Codex task

Use:

```text
workflows/codex-hermes-openhuman/templates/CODEX_TASK.template.md
```

Save as:

```text
tasks/<task-name>.md
```

For current active task, optionally copy to:

```text
CODEX_TASK.md
```

## Run Codex manually

Inside a git repo:

```bash
codex exec "Read CODEX_TASK.md, perform the task, and write AGENT_RESULT.md."
```

For longer tasks:

```bash
codex exec --full-auto "Read CODEX_TASK.md, perform the task, and write AGENT_RESULT.md."
```

Notes:
- Codex should run in a git repository.
- Use full-auto only when task scope is clear.
- Avoid yolo unless you intentionally want no guardrails.

## Review a Codex result

Hermes should inspect:

```text
AGENT_RESULT.md
git status
git diff
changed files
validation output
```

Then write:

```text
AGENT_REVIEW.md
```

or:

```text
reviews/<task-name>.md
```

## Promote memory candidates to OpenHuman

1. Hermes writes candidates to:

```text
memory/<topic>-memory-candidates.md
```

2. Human reviews and approves selected facts.

3. Hermes prepares an ingestion packet from:

```text
workflows/codex-hermes-openhuman/templates/OPENHUMAN_INGESTION.template.md
```

4. OpenHuman stores only approved stable facts.

## Common task prompts

### Repo inspection with OpenHuman loop

```text
按 codex-hermes-openhuman workflow 检查这个 repo：/Users/ai/projects/<repo>。开始前先读取 OpenHuman/memory context；不要修改源码；要求 Codex 输出 package manager、主要目录、测试命令、构建命令、潜在风险；结果写到 results/inspect-<repo>.md；结束后生成 memory/<repo>-memory-candidates.md。
```

### Feature implementation

```text
为 /Users/ai/projects/<repo> 创建 Codex task，实现 <feature>。开始前读取 OpenHuman context；限制 allowed files；验证命令是 <command>；结束后 review 并提取 OpenHuman memory candidates。
```

### Debugging

```text
创建 Codex debugging task。要求 Codex 先复现，再解释 root cause，再修复，再加 regression test。结束后只把可复用调试经验写成 memory candidates。
```

### Review

```text
Review the Codex result and current git diff. Write risks, quality gate status, next steps, and OpenHuman memory candidates if any.
```

## Maintenance cadence

Weekly or after major project work:
- archive completed tasks/results/reviews
- update AGENT_CONTEXT.md if repo conventions changed
- update OpenHuman context snapshots if durable facts changed
- extract stable memory candidates
- prune stale task files
- update templates if repeated gaps appear
