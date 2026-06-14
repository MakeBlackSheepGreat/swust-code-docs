# 配置 Schema

运行时主要读取 v1 配置字段，并在核心 v2 配置层中做迁移/适配。推荐用户配置使用 `swust-code.jsonc` 或 `.swust-code/swust-code.jsonc`。

## 常用字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `$schema` | string | 编辑器补全地址，当前代码写入 `https://opencode.ai/config.json` |
| `model` | string | 默认模型，格式为 `provider/model` |
| `small_model` | string | 标题生成等小任务模型 |
| `default_agent` | string | 默认 primary agent |
| `username` | string | 会话中显示的用户名 |
| `permission` | string 或 object | 工具权限规则 |
| `agent` | object | Agent 配置 |
| `provider` | object | 自定义 Provider 和模型覆盖 |
| `mcp` | object | MCP server 配置 |
| `command` | object | 自定义 slash command |
| `skills` | object | CLI/TUI v1 配置中的额外技能目录和 URL，结构为 `{ paths, urls }` |
| `instructions` | string[] | 额外指令文件或 glob |
| `plugin` | array | 外部插件 |
| `formatter` | boolean 或 object | 格式化配置 |
| `lsp` | boolean 或 object | LSP 配置 |
| `tool_output` | object | 工具输出截断阈值 |
| `compaction` | object | 上下文压缩配置 |
| `experimental.predict_next_prompt` | boolean | TUI 下一条输入预测开关，默认开启 |
| `share` | `manual`、`auto`、`disabled` | 会话分享策略 |

## 权限配置

```json
{
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow",
    "external_directory": {
      "*": "ask"
    },
    "doom_loop": "ask"
  }
}
```

权限值为 `allow`、`ask`、`deny`。字段可以直接写字符串，也可以写按资源模式匹配的对象。

## Agent 配置

```json
{
  "default_agent": "build",
  "agent": {
    "build": {
      "model": "anthropic/claude-sonnet-4-6",
      "permission": {
        "bash": "ask",
        "edit": "allow"
      }
    },
    "explore": {
      "mode": "subagent",
      "model": "openai/gpt-4o-mini"
    }
  }
}
```

内置 agent 包括 `build`、`plan`、`general`、`explore`、`compaction`、`title`、`summary`、`dream`、`distill`。

## MCP 配置

```json
{
  "mcp": {
    "docs": {
      "type": "remote",
      "url": "https://example.com/mcp"
    },
    "local-tools": {
      "type": "local",
      "command": ["node", "server.js"],
      "environment": {
        "TOKEN": "value"
      }
    }
  }
}
```

远程 MCP 默认支持 OAuth 流程；可用 `swust-code mcp auth <name>` 完成授权。

## 技能配置

当前 CLI/TUI 配置仍读取 v1 字段：

```json
{
  "skills": {
    "paths": [".swust-code/skills", "/absolute/path/to/skills"],
    "urls": ["https://example.com/.well-known/skills/"]
  }
}
```

core v2 配置层的 `skills` 是字符串数组，迁移层会把 v1 的 `paths` 和 `urls` 展开为数组。直接面向用户的配置文件建议继续使用上面的 v1 对象形式。

## 实验配置

```json
{
  "experimental": {
    "predict_next_prompt": false,
    "batch_tool": true,
    "openTelemetry": true
  }
}
```

`predict_next_prompt=false` 会关闭 TUI 的下一条输入预测。其他实验字段仍按运行时能力逐步接入。
