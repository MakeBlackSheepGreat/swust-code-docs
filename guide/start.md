# 快速开始

SWUST Code 是一个终端原生的 AI 编程助手，拥有持久记忆和自我进化能力。

## 安装

```bash
npm install -g swust-code
```

## 首次运行

```bash
swust-code
```

首次启动自动引导配置，选择 LLM 提供商并输入 API Key。

## 配置 API Key

```bash
# Anthropic（推荐）
export ANTHROPIC_API_KEY="your-key"

# OpenAI
export OPENAI_API_KEY="your-key"

# Google
export GOOGLE_API_KEY="your-key"
```

或在 TUI 内通过 `/providers` 命令配置。

## 基本用法

```bash
# 交互模式
swust-code

# 单次运行
swust-code run "解释这个项目"

# 自治模式（设定目标后自主工作）
swust-code run --goal "修复所有 TypeScript 错误" "开始工作"

# 知识提炼
swust-code dream

# 技能发现
swust-code distill
```

`dream` 和 `distill` 当前是 CLI 入口命令。代码里已经保留自动触发判断和专用 agent prompt，但自动周期调度函数仍返回 false，完整自动接入还在后续实现中。

## 记忆系统

SWUST Code 自动在 `~/.local/share/swust-code/memory/` 下维护记忆文件：

- `global/MEMORY.md` — 跨项目偏好
- `projects/<id>/MEMORY.md` — 项目知识
- `sessions/<id>/checkpoint.md` — 会话检查点

Agent 自动索引这些文件，在对话中检索相关知识。

当前核心 v2 工具注册表包含 `memory` 和 `memory_write`，用于搜索和写入持久记忆；TUI/旧会话路径仍保留自己的工具注册表，因此具体会话里展示的工具列表以运行时为准。

## 下一步

- [安装指南](/guide/install) — 详细的安装方式
- [配置](/guide/config) — 配置文件详解
- [LLM 提供商](/guide/providers) — 支持的模型和接入方式
- [持久化记忆](/features/memory) — 记忆系统详解
