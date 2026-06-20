# 快速开始

龙山灵码（SWUST Code）是基于 MiMo-Code 的终端原生 AI 编程智能体。它更适合真实仓库里的连续工作，而不是只做一轮问答。

## 适合什么任务

如果你的任务具有下面这些特征，龙山灵码通常更合适：

- 需要跨多个文件、多个阶段推进
- 需要把任务拆给子智能体，再把结果收回来
- 需要记住项目规则、架构约束和历史结论
- 需要在会话恢复后继续工作，而不是重新解释上下文

## 1. 安装

```bash
# 一键安装
curl -fsSL https://raw.githubusercontent.com/MakeBlackSheepGreat/swust-code/main/install | bash

# 或通过 npm 安装
npm install -g @swust-code/cli
```

安装后确认 CLI 可用：

```bash
swust-code --version
```

## 2. 首次启动

```bash
swust-code
```

首次启动会进入 Provider 配置向导。常见选项如下：

| 选项 | 适合场景 |
|------|----------|
| `MiMo Auto` | 想零配置开始使用 |
| `小米 MiMo 平台` | 想通过 MiMo OAuth 登录 |
| `从 Claude Code 导入` | 本机已有 Claude Code 凭证 |
| `自定义 Provider` | 使用 OpenAI 兼容网关或其他模型服务 |

Provider 和模型名称保持原名。`MiMo Auto`、`小米 MiMo 平台`、`mimo/mimo-auto`、`xiaomi/mimo-*` 都是服务商或模型标识。

如果你更习惯从终端管理 Provider：

```bash
swust-code providers list
swust-code providers login
swust-code providers import
```

## 3. 第一轮推荐使用路径

对于第一次在项目里使用龙山灵码，推荐按下面的顺序理解它：

1. 在项目根目录启动 `swust-code`
2. 先用默认主智能体理解仓库，再按需要切换到 `plan`、`compose` 或 `goal`
3. 如果任务有明确停止条件，使用 `/goal` 或 `swust-code run --goal ...`
4. 如果任务需要拆分、评审或并行处理，使用 `compose` 或 subagent
5. 在一个阶段结束后，用 `/dream` 或 `/distill` 沉淀长期知识和可复用流程

这条路径的重点是：龙山灵码不是只在“发一个 prompt”这一步发力，而是把任务推进、恢复和沉淀都放进同一条工作链里。

## 4. 常用命令

| 命令 | 用途 |
|------|------|
| `swust-code` | 启动交互式 TUI |
| `swust-code run "解释这个仓库"` | 从 shell 运行一次提示 |
| `swust-code run --goal "修复类型错误" "开始"` | 带停止条件的自治运行 |
| `/goal <目标>` | 在当前会话内设置停止条件 |
| `/memory <查询>` | 搜索持久化项目记忆 |
| `/subagent`、`/subagents` | 配置可见子智能体的模型、思考强度和最大步数 |
| `/dream` | 整理近期工作里值得长期保留的知识 |
| `/distill` | 把重复工作流沉淀为 skill、command、subagent 或 workflow |
| `/paste-image` | 从剪贴板附加图片 |
| `/model`、`/agent`、`/mcp`、`/skill`、`/effort` | 打开常用控制项或选择器 |

## 5. 配置文件与项目目录

龙山灵码同时使用配置文件和项目目录：

| 位置 | 用途 |
|------|------|
| `~/.config/swust-code/swust-code.json` | 全局运行时配置 |
| 项目根目录 `swust-code.json` | 项目运行时配置 |
| `~/.config/swust-code/tui.json` | 全局 TUI 配置 |
| 项目根目录 `tui.json` | 项目 TUI 配置 |
| 项目内 `.swust-code/` | Agent、Command、Skill、Workflow、Plugin 等项目级资产 |

常见的项目级目录包括：

- `.swust-code/agents/`
- `.swust-code/commands/`
- `.swust-code/skills/`
- `.swust-code/workflows/`
- `.swust-code/plugins/`

如果你只想做模型、权限、Agent 或 Provider 配置，通常先从 `swust-code.json` 开始；如果你想把项目自己的命令、技能或工作流放进仓库，再使用 `.swust-code/`。

## 6. 记忆、checkpoint 与恢复

龙山灵码会在本地维护长期项目记忆：

```text
~/.local/share/swust-code/memory/
  global/MEMORY.md
  projects/<project-id>/MEMORY.md
  projects/<project-id>/facts/<fact>.md
  sessions/<session-id>/checkpoint.md
  sessions/<session-id>/notes.md
  sessions/<session-id>/tasks/<task-id>/progress.md
```

这套结构服务于三件事：

- 让项目规则和事实可以跨会话保留
- 让长会话在接近上下文上限时仍能恢复
- 让子智能体的任务过程可以被主会话重新理解

如果你关心的是“AI 下一次还能不能接着干”，这里就是关键。

## 下一步

- [安装](/guide/install)
- [配置](/guide/config)
- [LLM 提供商](/guide/providers)
- [智能体模式](/features/agents)
- [持久化记忆](/features/memory)
- [工作流引擎](/features/workflow)
