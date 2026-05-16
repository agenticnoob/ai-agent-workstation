# AI Agent Workstation

[English](README.md) | 中文

这是一个本地 AI agent 工作站项目，用来保存和维护 Codex、Hermes Agent 与 OpenHuman 协作时使用的工作流、模板、任务交接文件、审查记录和长期记忆候选。

GitHub 项目地址：[agenticnoob/ai-agent-workstation](https://github.com/agenticnoob/ai-agent-workstation)

## 项目用途

这个仓库不是普通应用代码仓库，而是一个本地 AI 工程工作站的可审计工作区。它主要用于：

- 保存可复用的多 agent 工作流文档
- 管理 Hermes 给 Codex 的 Markdown handoff 模板
- 保存 Codex 执行结果与 Hermes review
- 暂存 OpenHuman 长期记忆候选与 ingestion packet
- 让本地 agent 工作方式可读、可审查、可回滚、可复用

## 目录结构

```text
templates/   通用可复用模板
tasks/       Codex 任务交接文件
results/     Codex 执行结果
reviews/     Hermes 审查记录
memory/      OpenHuman context snapshots 与长期记忆候选
workflows/   可复用多 agent 工作流定义
```

项目代码仓库默认不放在这里，而是按约定放在：

```text
/Users/ai/projects
```

## 当前主工作流

主工作流位于：

```text
workflows/codex-hermes-openhuman/
```

用于 Codex + Hermes Agent + OpenHuman 的本地协作。

默认流程：

```text
OpenHuman Recall → Hermes planning/review → Codex implementation/testing → Hermes review → OpenHuman Ingestion
```

## 默认角色分工

- Human/User：负责目标、约束、审批、风险容忍度和最终决策。
- Hermes Agent：负责上下文收集、任务规划、Codex handoff、结果审查和 memory candidate 提取。
- Codex CLI：负责代码修改、测试、构建、调试和结果报告。
- OpenHuman：负责稳定、非敏感事实的长期上下文和记忆。

## 默认 artifact flow

```text
OPENHUMAN_CONTEXT.md
  ↓
AGENT_CONTEXT.md
  ↓
CODEX_TASK.md 或 tasks/<task-name>.md
  ↓
AGENT_RESULT.md 或 results/<task-name>.md
  ↓
AGENT_REVIEW.md 或 reviews/<task-name>.md
  ↓
MEMORY_CANDIDATES.md 或 memory/<topic>-memory-candidates.md
  ↓
OPENHUMAN_INGESTION.md
```

## 使用方式

开始一个非平凡任务时，可以这样说：

```text
按 codex-hermes-openhuman workflow 执行。开始前读取 OpenHuman/memory context，结束后生成 OpenHuman memory candidates。
```

如果任务涉及某个代码仓库，建议明确提供 repo 路径和目标，例如：

```text
按 codex-hermes-openhuman workflow 检查这个 repo：/Users/ai/projects/example-app。不要修改源码；输出 package manager、主要目录、测试命令、构建命令和潜在风险。
```

## 安全默认值

- 工作流 artifact 保存在 `/Users/ai/agent-workspace`。
- 项目代码仓库默认保存在 `/Users/ai/projects`。
- 非平凡任务优先通过 Markdown 文件交接。
- 不把 secrets、token、cookie、私钥或 `.env` 内容写入 memory、OpenHuman packet 或模板。
- 高风险命令和外部集成需要明确确认。

## 相关链接

- GitHub 仓库：[agenticnoob/ai-agent-workstation](https://github.com/agenticnoob/ai-agent-workstation)
- 主工作流：[codex-hermes-openhuman](workflows/codex-hermes-openhuman/README.md)
- OpenHuman ingestion packet 示例：[memory/OPENHUMAN_INGESTION.md](memory/OPENHUMAN_INGESTION.md)
