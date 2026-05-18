# Codex + Hermes 工作流快速开始

Purpose: 用一页中文说明如何启动、执行和检查当前本地 Codex + Hermes 工作流。

Audience: 本人。这个文件是给人看的快速入口，不是 agent 操作规程。

## 一句话启动

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。
```

最小输入：

```text
目标：<要完成什么>
Repo：/Users/ai/projects/<repo-name>
约束：<哪些能改、哪些不能改、风险限制>
验证：<测试 / build / lint 命令>
期望输出：<result、review、是否可提交等>
```

快速版：

```text
在 /Users/ai/projects/<repo-name> 按 codex-hermes workflow 完成 <目标>，最小改动，完成后 review。
```

## 角色分工

- Human/User：目标、约束、风险接受度、凭证、最终批准。
- Hermes：上下文召回、规划、Codex handoff、结果 review、memory hygiene。
- Codex：repo 检查、代码修改、测试/构建/调试、结果报告。

## 标准流程

```text
1. Context recall
   Hermes 读取相关 memory、workflow docs、历史 artifacts 和 repo 状态。

2. Intake
   明确目标、工作目录、修改边界、验证命令、输出要求。

3. Handoff or direct action
   简单安全任务可直接做；复杂实现/调试任务先写 Codex task。

4. Codex implementation/testing
   Codex 在指定 repo 内执行，并写 result。

5. Hermes review
   Hermes 检查 result、git diff、changed files、validation output、越界风险。

6. Memory hygiene
   只保留稳定、非敏感、未来会复用的 memory candidates。
```

## Artifact flow

```text
AGENT_CONTEXT.md
  ↓
CODEX_TASK.md 或 tasks/<task-name>.md
  ↓
AGENT_RESULT.md 或 results/<task-name>.md
  ↓
AGENT_REVIEW.md 或 reviews/<task-name>.md
  ↓
MEMORY_CANDIDATES.md 或 memory/<topic>-memory-candidates.md
```

常用目录：

```text
/Users/ai/projects                    # 项目 repo 默认位置
/Users/ai/agent-workspace/tasks       # Codex handoff tasks
/Users/ai/agent-workspace/results     # Codex execution results
/Users/ai/agent-workspace/reviews     # Hermes reviews
/Users/ai/agent-workspace/memory      # memory candidates
/Users/ai/agent-workspace/workflows/codex-hermes
```

## Codex task 必须写清楚

使用 `templates/CODEX_TASK.template.md`，至少包含：

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

核心原则：范围明确、边界清楚、可验证、能写 result。

## Hermes review 必须检查

使用 `templates/AGENT_REVIEW.template.md`，重点检查：

- Codex 是否完成目标。
- 是否只修改允许范围内的文件。
- 是否运行约定的 test/build/lint。
- 失败或阻塞是否被诚实记录。
- git diff 是否合理。
- 是否误写入 secrets、凭证、临时日志。
- 是否有必要提取 memory candidates。

Verdict 只用三种：

```text
APPROVED
NEEDS_CHANGES
BLOCKED
```

## Memory hygiene

可以进入 memory candidates：

- 稳定的 repo 架构事实。
- 长期使用的技术栈、测试方式、项目约定。
- 未来多次会复用的工作流经验。
- 非敏感、不会一周内过期的信息。

不要进入 memory：

- 临时任务进度。
- issue / PR / commit 状态。
- 一次性错误输出。
- API key、token、cookie、SSH key、`.env` 内容。
- 很快会过期的结果。

## 常用启动模板

### 先调研 repo，不改代码

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。

目标：检查 /Users/ai/projects/<repo> 的项目结构、技术栈、测试命令、构建命令和当前 git 状态。
约束：不要修改任何源文件。
输出：写 result，然后由 Hermes review，告诉我下一步最适合做什么。
```

### 实现功能

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。

目标：实现 <功能描述>。
Repo：/Users/ai/projects/<repo>
约束：只允许修改 <路径>；不要修改 <路径>；不要引入全局依赖。
验证：运行 <test/build/lint 命令>。
输出：Codex 写 result，Hermes 写 review，并告诉我是否可以提交。
```

### 修 bug

```text
按 codex-hermes workflow 执行。

目标：修复 <错误信息 / bug 现象>。
Repo：/Users/ai/projects/<repo>
复现方式：<命令或步骤>
约束：优先最小修改；不要大重构。
验证：<复现命令应通过；相关测试应通过>
输出：Codex 写修复报告，Hermes review diff。
```

### 只审查，不修改

```text
按 codex-hermes workflow 执行。

目标：审查 /Users/ai/projects/<repo> 当前改动，不修改代码。
范围：检查 git diff、测试风险、架构问题、潜在 bug。
输出：写 review 到 /Users/ai/agent-workspace/reviews/<task-name>.md，并给 verdict。
```

## 文档维护原则

这个 workflow 故意保持小而清楚：

- `README.md`：目录入口和 source-of-truth 摘要。
- `QUICKSTART.zh-CN.md`：给人看的日常使用说明。
- `AGENT_RUNBOOK.md`：给 Hermes/Codex 看的执行备忘。
- `templates/`：实际会被 artifact flow 使用的模板。

不要为角色、架构、runbook、quality gates 再拆多个文件，除非这些内容明显增长到一页说明无法承载。
