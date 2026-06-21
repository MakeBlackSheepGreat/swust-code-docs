---
layout: home

hero:
  name: 龙山灵码
  text: "SWUST Code"
  tagline: "基于 MiMo-Code 的终端 AI 编程工具。当前主线继承 MiMo-Code 的记忆、checkpoint、subagent、goal、compose、MCP、LSP 和插件能力，并补充中文 TUI、工程防护和项目级子智能体配置。"
  actions:
    - theme: brand
      text: 快速开始
      link: /guide/start
    - theme: alt
      text: 主线状态
      link: /mainline-status
    - theme: alt
      text: SWUST 优势
      link: /DIFFERENCES

features:
  - title: MiMo-Code 基座
    details: "当前主线继承 MiMo-Code 的运行时能力。MiMo 已有的功能按 MiMo 原生实现为准。"
    link: /mainline-status
  - title: 项目记忆与 checkpoint
    details: "使用 MEMORY.md、facts、checkpoint.md 和 task progress 保存项目事实、会话状态和任务进度。"
    link: /features/memory
  - title: 多智能体运行
    details: "build、plan、compose、goal 和 subagent 用于不同阶段的分析、执行、编排和验证。"
    link: /features/agents
  - title: 工程防护
    details: "Task Gate、Bash Safety、Write Guard 和 Document Validation 分别处理提前停止、危险命令、越界写入和文档结构错误。"
    link: /features/security
  - title: 工作流与沉淀
    details: "workflow 用于可恢复的多阶段任务；dream 和 distill 用于整理项目知识和重复流程。"
    link: /features/workflow
  - title: 中文 TUI
    details: "中文命令说明、侧边栏信息和主题配置面向中文开发者的日常终端使用。"
    link: /features/tui
---

## 先读哪一页

| 你要做什么 | 入口 |
|------------|------|
| 安装并完成第一次启动 | [快速开始](/guide/start) |
| 确认当前主线基于什么 | [主线状态](/mainline-status) |
| 理解 SWUST 相对 MiMo 的新增部分 | [SWUST 优势](/DIFFERENCES) |
| 理解 Agent、subagent、goal、compose 的关系 | [智能体模式](/features/agents) |
| 理解记忆和 checkpoint 如何恢复上下文 | [持久化记忆](/features/memory) |
| 查看 CLI 和配置细节 | [CLI 命令](/api/commands)、[配置 Schema](/api/config-schema) |

## 基本事实

| 项目 | 当前说明 |
|------|----------|
| 中文名 | 龙山灵码 |
| 英文名 | SWUST Code |
| CLI 命令 | `swust-code` |
| 当前声明版本 | `v0.6.0` |
| 运行时基座 | MiMo-Code |
| 项目目录 | `.swust-code/` |
| 运行时配置 | `swust-code.json` 或 `swust-code.jsonc` |

## 适用范围

SWUST Code 更适合在已有仓库中处理需要多轮推进的任务，例如：

- 修复一组类型错误、测试错误或构建错误
- 分阶段完成重构、升级或功能实现
- 调用子智能体做调查、实现、评审或验证
- 在多次会话之间保留项目规则和已完成进度

它不是专门为一次性问答设计的聊天界面。如果任务只需要简短解释，普通对话工具通常更直接。

## 和 MiMo-Code 的关系

当前维护原则很简单：

1. MiMo-Code 已有能力，优先保留 MiMo 原生实现。
2. MiMo-Code 没有的能力，再加入 SWUST 层。
3. Provider 和模型名称保持原名，例如 `MiMo Auto`、`mimo/mimo-auto`、`xiaomi/mimo-*`。

这条原则用于避免把当前主线改回旧 OpenCode 风格，也用于区分“继承能力”和“SWUST 新增能力”。
