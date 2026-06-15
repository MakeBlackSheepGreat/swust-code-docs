# CLI 命令

## 全局参数

| 参数 | 说明 |
|------|------|
| `--help`, `-h` | 显示帮助 |
| `--version`, `-v` | 显示版本 |
| `--print-logs` | 将日志输出到 stderr |
| `--log-level DEBUG\|INFO\|WARN\|ERROR` | 设置日志级别 |
| `--pure` | 禁用外部插件 |

## 基本命令

| 命令 | 说明 |
|------|------|
| `swust-code` | 启动交互式 TUI |
| `swust-code run [message]` | 运行单次命令 |
| `swust-code run --goal "目标" "消息"` | 自治模式，默认路由到 `goal` Agent |
| `swust-code run --agent compose "消息"` | 进入 compose 智能体模式 |
| `swust-code dream` | 启动记忆整合自治 run |
| `swust-code distill` | 启动工作流打包自治 run |
| `swust-code serve` | 启动 headless API server |
| `swust-code web` | 启动 server 并打开 Web UI |
| `swust-code attach <url>` | 连接已有 server |
| `swust-code --help` | 显示帮助 |
| `swust-code --version` | 显示版本 |

## run 命令

```bash
swust-code run [message..]

选项:
  -c, --continue          继续上一个会话
  -s, --session           指定会话 ID
  -m, --model             指定模型 (provider/model)
  --goal                  设定自治目标；未指定 --agent 时使用 goal Agent
  --agent                 指定智能体，例如 compose、goal 或自定义 Agent
  --fork                  分叉会话后再继续
  --share                 分享会话
  --format default|json   输出格式
  -f, --file              附加文件
  --title                 指定会话标题
  --attach                连接远端 server
  --dir                   指定运行目录
  --interactive, -i       启动直接交互模式
  --thinking              显示 thinking block
  --variant               指定模型变体
  --dangerously-skip-permissions  自动批准未显式拒绝的权限
```

## 管理命令

| 命令 | 说明 |
|------|------|
| `swust-code providers list` | 列出 Provider 凭证 |
| `swust-code providers login [url]` | 登录 Provider |
| `swust-code providers logout [provider]` | 删除 Provider 凭证 |
| `swust-code providers import` | 从 MiMo-Code、Claude Code 或环境变量导入凭证 |
| `swust-code agent` | 管理智能体 |
| `swust-code mcp list` | 列出 MCP 服务器 |
| `swust-code mcp add` | 添加 MCP 服务器 |
| `swust-code mcp auth [name]` | 为远程 MCP 执行 OAuth |
| `swust-code mcp logout [name]` | 删除 MCP OAuth 凭证 |
| `swust-code models [provider]` | 列出模型 |
| `swust-code plugin <module>` | 安装插件 |
| `swust-code session` | 管理会话 |
| `swust-code db` | 数据库工具 |
| `swust-code stats` | 查看 token 与费用统计 |
| `swust-code export [sessionID]` | 导出会话 JSON |
| `swust-code import <file>` | 导入会话 JSON 或分享 URL |
| `swust-code github` | 管理 GitHub agent |
| `swust-code pr <number>` | 拉取并 checkout PR 后运行龙山灵码 |
| `swust-code acp` | 启动 Agent Client Protocol server |
| `swust-code upgrade` | 升级 |
| `swust-code uninstall` | 卸载 |

## dream / distill 命令

两个命令都会复用自治任务 runner，并启动 `swust-code run --goal ...`。

```bash
swust-code dream [options]
swust-code distill [options]

选项:
  --dry-run              只展示任务文本，不启动 Agent
  -y, --yes             跳过确认
  -m, --model           指定模型 (provider/model)
  --agent               指定 primary agent
  --dir                 指定运行目录
```

后台自动触发时使用 `--yes --dir <cwd>`，并通过 `SWUST_CODE_AUTO_EVOLUTION=0` 防止递归触发。
