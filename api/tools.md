# 工具参考

SWUST Code 当前有两套工具注册路径：核心 v2 runner 使用 `packages/core/src/tool/`，TUI/旧会话路径使用 `packages/opencode/src/tool/`。实际会话中展示的工具以运行时路径为准。

## Core v2 内置工具

| 工具 | 说明 | 备注 |
|------|------|------|
| `bash` | 执行 shell 命令 | 内置安全分析，默认超时 2 分钟 |
| `read` | 读取文件或图片 | 支持文件系统读取 |
| `write` | 写入文件 | 使用 `edit` 权限动作 |
| `edit` | 精确编辑文件 | 使用 `edit` 权限动作 |
| `apply_patch` | 应用补丁 | GPT 系模型优先使用 |
| `glob` | 文件模式搜索 | 基于 glob |
| `grep` | 内容搜索 | 基于 ripgrep |
| `webfetch` | 获取网页内容 | 有响应大小上限 |
| `websearch` | 网络搜索 | 按 Provider/运行时能力启用 |
| `memory` | 搜索持久记忆 | FTS5 + BM25 |
| `memory_write` | 写入持久记忆 | 支持 global/projects/sessions |
| `todowrite` | 任务状态管理 | 用于任务看板 |
| `question` | 向用户提问 | 由运行时开关控制 |
| `skill` | 加载 SKILL.md | 会返回技能正文和采样文件列表 |
| `history` | 搜索历史会话 | 基于 History FTS |

## TUI/旧会话工具

| 工具 | 说明 |
|------|------|
| `shell` / `bash` | 执行 shell 命令，工具 ID 由 ShellID 决定 |
| `read`、`write`、`edit`、`apply_patch` | 文件读写和补丁 |
| `glob`、`grep` | 文件搜索和内容搜索 |
| `task` | 派生子智能体，可选后台运行 |
| `actor` | MiMo 风格 Actor API：run、spawn、status、wait、cancel、send |
| `subagent` | 专用子 Agent 派发工具 |
| `workflow` | 调用脚本化工作流 |
| `memory` | 搜索或写入记忆 |
| `history` | 查询历史会话和片段 |
| `webfetch`、`websearch` | 网页获取和搜索 |
| `skill` | 加载技能 |
| `lsp` | 实验性 LSP 工具 |
| `plan_exit` | 实验性 Plan 模式退出工具 |

## 安全属性

核心 v2 工具声明三个安全属性：

- `isReadOnly`：只读操作
- `isConcurrencySafe`：可并行执行
- `isDestructive`：是否具备破坏性，默认 true

## Bash 安全

Bash 工具内置安全分析器，自动标记 `safe`、`caution`、`dangerous` 三类风险。高风险示例包括递归删除、管道执行脚本、`eval`、`chmod 777`、文件系统格式化、fork bomb、`kill -9 -1` 等。详见[安全防护](/features/security)。

## Actor 工具

v0.4 的 `actor` 工具暴露 MiMo 风格 Actor API：

| 操作 | 说明 |
|------|------|
| `run` | 前台运行子 Agent，等待结果 |
| `spawn` | 后台运行子 Agent，返回 actor id |
| `status` | 查询 registry 中的 actor 状态 |
| `wait` | 等待后台 actor 完成 |
| `cancel` | 取消 actor |
| `send` | 通过 Inbox 向 actor 发送消息 |

后台 actor 的结果会进入可等待 outcome；任务型 actor 会按 return header 和 Task Registry 更新状态。
