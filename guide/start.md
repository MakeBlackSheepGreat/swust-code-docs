# 快速开始

龙山灵码（SWUST Code）是基于 MiMo-Code 的终端原生 AI 编程智能体。它适合处理需要多轮推进的软件工程任务：读写代码、运行命令、使用 MCP / LSP / 插件、维护长期项目记忆，并通过 goal、compose、subagent 和 checkpoint 支持长任务连续工作。

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

首次启动会进入 Provider 配置向导。

| 选项 | 适用场景 |
|------|----------|
| MiMo Auto | 希望零配置开始使用限时免费通道 |
| 小米 MiMo 平台 | 希望通过 MiMo OAuth 登录 |
| 从 Claude Code 导入 | 本机已有 Claude Code 凭证 |
| 自定义 Provider | 使用 OpenAI 兼容网关或其他模型服务商 |

Provider 和模型名称保持原样。`MiMo Auto`、`小米 MiMo 平台`、`mimo/mimo-auto`、`xiaomi/mimo-*` 是服务商或模型 ID，不会被改名。

## 3. 常用 Provider 环境变量

也可以直接通过环境变量接入常见服务商：

```bash
export ANTHROPIC_API_KEY="your-key"
export OPENAI_API_KEY="your-key"
export GOOGLE_API_KEY="your-key"
```

需要查看或登录 Provider：

```bash
swust-code providers list
swust-code providers login
swust-code providers login --provider xiaomi
```

## 4. 日常命令

| 命令 | 用途 |
|------|------|
| `swust-code` | 启动交互式 TUI |
| `swust-code run "解释这个仓库"` | 从 shell 运行一次提示 |
| `swust-code run --goal "修复类型错误" "开始"` | 带自治停止条件运行 |
| `/goal <目标>` | 在 TUI 内设置停止条件 |
| `/memory <查询>` | 搜索持久化项目记忆 |
| `/dream` | 整理可长期保留的项目知识 |
| `/distill` | 将重复工作流沉淀为 skill、subagent 或 command |
| `/paste-image` | 从剪贴板附加图片 |
| `/model`、`/agent`、`/mcp`、`/skill`、`/effort` | 打开常用 TUI 控件别名 |

## 5. 记忆与 checkpoint

龙山灵码会在本机维护跨会话记忆：

```text
~/.local/share/swust-code/memory/
  global/MEMORY.md
  projects/<project-id>/MEMORY.md
  projects/<project-id>/facts/<fact>.md
  sessions/<session-id>/checkpoint.md
  sessions/<session-id>/notes.md
  sessions/<session-id>/tasks/<task-id>/progress.md
```

记忆通过 SQLite FTS5 搜索，并在会话恢复或接近上下文上限时和 checkpoint 一起重建上下文。`/dream` 用于整理长期项目知识，`/distill` 用于从重复操作中提炼可复用工作流。

## 6. 配置文件

运行时配置使用 `swust-code.json` 或 `swust-code.jsonc`：

```jsonc
{
  "model": "anthropic/claude-sonnet-4-6",
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow"
  }
}
```

常见位置：

| 类型 | 路径 |
|------|------|
| 全局运行时配置 | `~/.config/swust-code/swust-code.json` |
| 项目运行时配置 | 项目根目录的 `swust-code.json` |
| 全局 TUI 配置 | `~/.config/swust-code/tui.json` |
| 项目 TUI 配置 | 项目根目录的 `tui.json` |

## 下一步

- [安装指南](/guide/install)
- [配置说明](/guide/config)
- [LLM 提供商](/guide/providers)
- [持久化记忆](/features/memory)
- [CLI 命令](/api/commands)
