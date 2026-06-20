# 配置

龙山灵码通过 JSON/JSONC 配置文件管理模型、权限、Provider、MCP、Agent、插件和 TUI 行为。

## 配置文件位置

| 范围 | 路径 |
|------|------|
| 全局级 | `~/.config/swust-code/swust-code.json`、`~/.config/swust-code/swust-code.jsonc` |
| 项目级 | `swust-code.json`、`swust-code.jsonc`（从当前目录向上查找） |
| 项目目录 | `.swust-code/swust-code.json`、`.swust-code/swust-code.jsonc` |
| TUI | `~/.config/swust-code/tui.json`、项目根目录 `tui.json`，也支持 `tui.jsonc` |

项目级配置优先于全局配置；更靠近当前工作目录的配置优先级更高。可以用 `SWUST_CODE_CONFIG` 指定单个配置文件，用 `SWUST_CODE_CONFIG_DIR` 指定额外配置目录。

## 基本配置

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-4-6",
  "shell": "/bin/bash",
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow"
  }
}
```

## 模型配置

```json
{
  "model": "anthropic/claude-sonnet-4-6",
  "default_agent": "build",
  "agent": {
    "build": {
      "model": "anthropic/claude-opus-4-8"
    },
    "explore": {
      "model": "anthropic/claude-haiku-4-5-20251001"
    }
  }
}
```

## 权限配置

```json
{
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow",
    "glob": "allow",
    "grep": "allow",
    "memory": "allow",
    "memory_write": "ask"
  }
}
```

权限值：`allow`（自动允许）、`ask`（每次询问）、`deny`（拒绝）。`write` 与 `edit` 在运行时共享编辑权限，通常配置 `edit` 即可。

## MCP 服务器

```json
{
  "mcp": {
    "my-server": {
      "type": "remote",
      "url": "https://example.com/mcp"
    }
  }
}
```

## 技能来源

```json
{
  "skills": {
    "paths": [".swust-code/skills"],
    "urls": ["https://example.com/.well-known/skills/"]
  }
}
```

当前 CLI/TUI 读取的是 v1 对象形式；core v2 内部会把这些来源适配为本地目录或远端 URL。

## 实验选项

```json
{
  "experimental": {
    "predict_next_prompt": true
  }
}
```

`predict_next_prompt` 控制 TUI 下一条输入预测。默认开启；设为 `false` 后，空输入框不会再显示 ghost suggestion。

## 环境变量

| 变量 | 说明 |
|------|------|
| `SWUST_CODE_CONFIG` | 指定单个配置文件 |
| `SWUST_CODE_CONFIG_DIR` | 自定义配置目录 |
| `SWUST_CODE_CONFIG_CONTENT` | 用环境变量注入配置内容 |
| `SWUST_CODE_DISABLE_PROJECT_CONFIG` | 禁用项目级配置 |
| `SWUST_CODE_DB` | 自定义数据库路径 |
| `SWUST_CODE_PURE` | 禁用外部插件 |
| `SWUST_CODE_DISABLE_MODELS_FETCH` | 禁止刷新模型目录 |
| `SWUST_CODE_SERVER_PASSWORD` | `serve`/`web` 的服务认证密码 |
| `SWUST_CODE_SERVER_USERNAME` | `serve`/`web` 的服务认证用户名 |
| `SWUST_CODE_LOCALE` | 固定 TUI 语言偏好，可设为 `auto`、`en`、`zh` 等 |
| `SWUST_CODE_AUTO_EVOLUTION` | 设置为 `0` 或 `false` 时禁用 Dream/Distill 后台自动触发 |
| `SWUST_CODE_MEMORY_RECONCILE_ON_SEARCH` | 搜索前自动同步记忆（默认 true） |
| `SWUST_CODE_MEMORY_SEARCH_SCORE_FLOOR` | 记忆搜索分数阈值（默认 0.15） |
