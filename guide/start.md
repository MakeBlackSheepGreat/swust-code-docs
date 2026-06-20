# 快速开始

龙山灵码是一个终端原生的 AI 编程助手，拥有持久记忆和自我进化能力。

## 安装

```bash
npm install -g @swust-code/cli
```

## 首次运行

```bash
swust-code
```

首次启动会自动引导配置。可选择 MiMo Auto（限时免费）、小米 MiMo 平台、从 Claude Code 导入认证，或添加任意 OpenAI 兼容 Provider。

## 配置 API Key

```bash
# Anthropic（推荐）
export ANTHROPIC_API_KEY="your-key"

# OpenAI
export OPENAI_API_KEY="your-key"

# Google
export GOOGLE_API_KEY="your-key"
```

或在 TUI 内通过首次启动向导和 Provider 配置入口完成。

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

`dream` 和 `distill` 会启动带 `--goal` 的自治 run。普通会话结束后，系统也会按 7 天 Dream、30 天 Distill 的间隔检查是否需要后台触发；可用 `SWUST_CODE_AUTO_EVOLUTION=0` 禁用自动进化。

## 记忆系统

龙山灵码自动在 `~/.local/share/swust-code/memory/` 下维护记忆文件：

- `global/MEMORY.md` — 跨项目偏好
- `projects/<id>/MEMORY.md` — 项目知识
- `sessions/<id>/checkpoint.md` — 会话检查点

Agent 会自动索引这些文件，并在对话中检索相关知识。需要手动整理知识时，可以使用 `dream` 提炼项目记忆，也可以让 Agent 通过记忆工具搜索或写入长期信息。

## 下一步

- [安装指南](/guide/install) — 详细的安装方式
- [配置](/guide/config) — 配置文件详解
- [LLM 提供商](/guide/providers) — 支持的模型和接入方式
- [持久化记忆](/features/memory) — 记忆系统详解
