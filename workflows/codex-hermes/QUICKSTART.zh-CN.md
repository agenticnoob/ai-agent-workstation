# Codex + Hermes 工作流快速开始

Purpose: 一页中文快速入口。
Audience: 人类操作者。这个文件不是 agent 操作规程。

## 一句话启动

```text
按 codex-hermes workflow 执行。开始前读取本地 memory/context，结束后生成 Hermes memory candidates。
```

## 最小输入

```text
目标：<要完成什么>
Repo：/Users/ai/projects/<repo-name>
约束：<能改什么 / 不能改什么 / 风险限制>
验证：<测试 / build / lint 命令>
期望输出：<result / review / 是否可提交>
```

## 角色分工

- Human/User：目标、约束、风险接受度、凭证、最终批准
- Hermes：上下文召回、规划、Codex handoff、review、memory hygiene
- Codex：repo 检查、代码修改、测试 / 构建 / 调试、结果报告

## 标准流程

```text
1. Context recall
   只读与当前任务有关的 memory、workflow docs、历史 artifacts 和 repo 状态。

2. Intake
   确认目标、工作目录、修改边界、验证命令、输出要求。

3. Handoff or direct action
   简单安全任务可直接做；复杂实现 / 调试任务先写 Codex task。

4. Codex implementation/testing
   Codex 在指定 repo 内执行，并写 result。

5. Hermes review
   Hermes 检查 result、git diff、changed files、validation output 和越界风险。

6. Memory hygiene
   只保留稳定、非敏感、可复用的 memory candidates。
```

## 常用目录

```text
/Users/ai/projects                    # 项目 repo 默认位置
/Users/ai/agent-workspace/tasks       # Codex handoff tasks
/Users/ai/agent-workspace/results     # Codex execution results
/Users/ai/agent-workspace/reviews     # Hermes reviews
/Users/ai/agent-workspace/memory      # memory candidates
/Users/ai/agent-workspace/workflows/codex-hermes
```

## Codex task 最小要求

Goal / Context / Working Directory / Allowed Files / Do Not Touch / Steps / Validation / Expected Output / Result File / Safety Notes

优先使用 `my-agents-mcp` 生成 skeleton/template；如果 MCP 不可用，再用 `templates/CODEX_TASK.template.md` 复制填写。`templates/*.template.md` 只是 fallback，不要原样交给 Codex。

## 常用启动模板

### 先调研，不改代码

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

## 维护说明

- `README.md`：目录入口和 source-of-truth 摘要
- `AGENT_RUNBOOK.md`：agent 执行备忘
- `QUICKSTART.zh-CN.md`：人类日常入口
- `templates/`：真正会被 flow 使用的模板

不要再拆出更多平行文档，除非内容真的大到一页放不下。
