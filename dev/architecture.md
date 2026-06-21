# 架构设计

龙山灵码由终端界面、任务编排、会话运行时、工具系统和项目状态存储组成。开发者可以先按职责理解系统，再进入具体包目录。

## 五层视角

```text
Interface Layer
  CLI / TUI / Web / Desktop / API server

Extension Layer
  Plugins / Skills / MCP / custom commands / integration surfaces

Coordination Layer
  Agent orchestration / subagents / workflow / goal / compose

Execution Layer
  Session runtime / tool registry / permissions / model routing / context rebuild

Foundation Layer
  Effect services / SQLite + Drizzle / config / filesystem / project state
```

这张图用于说明职责边界，不对应每个源码文件的精确目录位置。

## Monorepo 分工

| 包组 | 主要职责 |
|------|----------|
| `opencode` | 主运行时、CLI、会话、工具、配置、服务端路由 |
| `app` / `desktop` / `web` / `console` | 用户界面与交互入口 |
| `sdk` / `ui` / `shared` | 公共类型、组件、共享能力 |
| `plugin` / `extensions` / `function` | 扩展与运行时对接面 |
| `script` / `containers` / `identity` / `enterprise` / `slack` / `storybook` | 构建、集成、部署和周边能力 |

## 关键路径

### 会话运行

会话运行时负责组装输入、选择模型、调用工具、处理权限并记录消息。长任务会同时使用记忆、checkpoint 和上下文重建。

### 智能体编排

主智能体、subagent、`goal`、`compose` 和 workflow 共享任务状态与工具边界。subagent 的结果会回到主任务链路，workflow 则把多阶段执行写成可恢复流程。

### 工程防护

Task Gate、Bash Safety、Write Guard 和 Document Validation 会影响实际执行边界。它们分别处理提前停止、高风险 shell 命令、写入路径和结构化文档修改。

## 阅读顺序

如果你要继续理解代码结构，建议先读：

1. [智能体模式](/features/agents)
2. [持久化记忆](/features/memory)
3. [工作流引擎](/features/workflow)
4. [安全防护](/features/security)
5. [配置 Schema](/api/config-schema)
