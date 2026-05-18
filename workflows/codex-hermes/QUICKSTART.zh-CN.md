# Codex + Hermes 工作流快速开始

Purpose: 用一页中文说明如何启动和执行本地 Codex + Hermes 工作流，方便日后快速查看和复制使用。

Audience: 徐力本人、Hermes Agent，以及需要按本流程执行的 Codex task runner。

## 一句话启动

把下面这句话发给 Hermes：

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。
```

然后补充目标、repo、约束、验证方式和期望输出即可。

## 最小输入格式

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。

目标：
<要完成什么>

Repo：
/Users/ai/projects/<repo-name>

约束：
<哪些文件能改、哪些不能改、风险限制>

验证：
<要运行的测试 / build / lint 命令>

期望输出：
<Codex result、Hermes review、是否可提交等>
```

如果只是快速启动，也可以说：

```text
在 /Users/ai/projects/<repo-name> 按 codex-hermes workflow 完成 <目标>，最小改动，完成后 review。
```

## 角色分工

- Human/User：决定目标、约束、风险接受度、凭证和最终批准。
- Hermes Agent：读取上下文、规划、写 Codex handoff、review Codex 结果、整理 memory candidates。
- Codex CLI：检查 repo、修改代码、运行测试/构建/调试、写执行结果报告。
- Hermes built-in memory：只保存稳定、非敏感、未来会复用的长期事实。

## 标准执行流程

```text
1. Local context recall
   Hermes 读取 memory、workflow docs、历史 task/result/review、repo 状态。

2. Intake
   明确目标、工作目录、修改边界、验证命令、输出要求、风险等级。

3. Planning / Handoff
   简单任务可直接执行；复杂任务先写 Codex task。

4. Codex implementation/testing
   Codex 在指定 repo 内实现、测试、构建、调试，并写 result。

5. Hermes review
   Hermes 检查 result、git diff、changed files、validation output、越界风险。

6. Memory hygiene
   只提取稳定、非敏感、跨 session 有价值的信息作为 memory candidates。

7. Next step
   Hermes 给出一个明确的下一步建议。
```

## 常用文件流

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
/Users/ai/projects                    # 项目代码 repo 默认位置
/Users/ai/agent-workspace/tasks       # Codex handoff tasks
/Users/ai/agent-workspace/results     # Codex execution results
/Users/ai/agent-workspace/reviews     # Hermes reviews
/Users/ai/agent-workspace/memory      # memory candidates
/Users/ai/agent-workspace/workflows/codex-hermes  # 当前工作流说明
```

## 模板 A：实现功能

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。

目标：
实现 <功能描述>。

Repo：
/Users/ai/projects/<repo>

约束：
只允许修改 <路径>。
不要修改 <路径>。
不要引入新的全局依赖。

验证：
运行 <test/build/lint 命令>。

期望输出：
Codex 写 result，Hermes 写 review，并告诉我是否可以提交。
```

## 模板 B：只审查，不修改

```text
按 codex-hermes workflow 执行。

目标：
审查 /Users/ai/projects/<repo> 当前改动，不修改代码。

范围：
检查 git diff、测试风险、架构问题、潜在 bug。

输出：
写 review 到 /Users/ai/agent-workspace/reviews/<task-name>.md。
最后给 verdict：APPROVED / NEEDS_CHANGES / BLOCKED。
```

## 模板 C：先调研 repo，不改代码

```text
按 codex-hermes workflow 执行。

目标：
检查 /Users/ai/projects/<repo> 的项目结构、技术栈、测试命令、构建命令和主要风险。

约束：
不要修改任何源文件。

输出：
写 context/result 到 /Users/ai/agent-workspace/results/<repo>-inspection.md。
给我后续建议。
```

## 模板 D：修 bug

```text
按 codex-hermes workflow 执行。

目标：
修复这个问题：
<粘贴错误信息 / bug 现象>

Repo：
/Users/ai/projects/<repo>

复现方式：
<命令或步骤>

约束：
优先最小修改；不要大重构。

验证：
<复现命令应通过；相关测试应通过>

输出：
Codex 写修复报告，Hermes review diff。
```

## Hermes 创建 Codex task 时应包含的内容

```text
# Codex Task

## Goal
## Context
## Working Directory
## Allowed Files
## Do Not Touch
## Steps
## Validation
## Expected Output
## Result File
## Safety Notes
```

Codex task 的核心原则：范围明确、边界清楚、可验证、能写 result。

## Hermes review 应检查什么

- Codex 是否完成目标。
- 是否只修改了允许范围内的文件。
- 是否运行了约定的测试 / build / lint。
- 失败是否被诚实记录。
- git diff 是否合理。
- 是否有 secrets、凭证、临时日志被误写入。
- 是否需要 memory candidates。

Review verdict 只用三种：

```text
APPROVED
NEEDS_CHANGES
BLOCKED
```

## Memory hygiene 原则

可以进入 memory candidates 的内容：

- 稳定的 repo 架构事实。
- 项目长期使用的技术栈和测试方式。
- 未来多次会复用的工作流经验。
- 非敏感、不会一周内过期的信息。

不要进入 memory 的内容：

- 临时任务进度。
- issue / PR / commit 状态。
- 一次性错误输出。
- API key、token、cookie、SSH key、`.env` 内容。
- 很快会过期的结果。

## 推荐第一次使用方式

先做低风险 repo inspection：

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。

目标：
先检查 /Users/ai/projects/<repo> 的项目结构、测试命令、构建命令和当前 git 状态，不修改代码。

输出：
生成一个 repo inspection result，然后由 Hermes review，告诉我下一步最适合做什么。
```

这样可以先建立项目上下文，再进入具体实现，风险最低。

## 相关文档

- `/Users/ai/agent-workspace/workflows/codex-hermes/README.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes/WORKFLOW.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes/HANDOFF_PROTOCOL.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes/QUALITY_GATES.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes/RUNBOOK.md`
