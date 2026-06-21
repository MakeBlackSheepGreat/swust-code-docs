# 主线状态

当前声明版本：`v0.6.0`

代码仓库：<https://github.com/MakeBlackSheepGreat/swust-code>

## 当前版本

v0.6.0 基于 MiMo-Code。MiMo-Code 已经提供的运行时能力继续沿用原实现，包括记忆、checkpoint、actor / subagent、`goal`、`compose`、Dream / Distill、MCP、LSP、插件和 TUI / Server Runtime。

SWUST 层主要增加这些内容：

- 中文优先的 TUI 文案和信息组织
- 更完整的侧边栏上下文
- Task Gate、Bash Safety、Write Guard
- Document Validation 和 cache-stable 上下文布局
- `@path` 记忆导入和 one-fact-per-file 事实存储
- `/memory`、`/paste-image`、`/subagent`、`/subagents`

## 适用边界

| 工作类型 | 状态 |
|----------|------|
| 真实仓库内的多轮编码任务 | 适合 |
| 长任务恢复、续跑、分阶段推进 | 适合 |
| 子智能体拆分、复核、并行执行 | 适合 |
| 项目知识沉淀与长期记忆维护 | 适合 |
| 一次性浅层问答 | 不是主要目标 |

## 版本口径

文档中提到 memory、checkpoint、subagent、`goal`、`compose`、Dream / Distill 等能力时，默认表示 v0.6.0 继承 MiMo-Code 的实现。只有 Task Gate、Bash Safety、Write Guard、Document Validation、`/subagent` 项目级配置等明确由 SWUST 增加或调整的内容，才写作 SWUST 层能力。

Provider 和模型名称保持原名：

- `MiMo Auto`
- `小米 MiMo 平台`
- `mimo/mimo-auto`
- `xiaomi/mimo-*`

这些名称是服务商或模型标识，配置和文档中都保留原名。

## 继续阅读

- [快速开始](/guide/start)
- [SWUST 优势](/DIFFERENCES)
- [智能体模式](/features/agents)
- [持久化记忆](/features/memory)
- [工作流引擎](/features/workflow)
