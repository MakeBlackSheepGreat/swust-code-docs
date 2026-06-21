# 架构设计

## 当前架构怎么理解

龙山灵码当前主线以 MiMo-Code 为运行时基座，再叠加 SWUST 的产品层增强。可以先从四个职责理解这套分层：

- 接口层要同时服务 CLI / TUI / Web / Desktop / API
- 编排层要让主智能体、subagent、workflow、goal 共享同一套运行时
- 执行层要统一处理 session、tool、permission、model、context rebuild
- 基础层要稳定提供配置、文件系统、数据库和项目状态

这也是为什么记忆、checkpoint、任务状态和子智能体不会被做成互不相干的功能点。

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

这张图用于说明当前主线的职责边界，不对应每个源码文件的精确目录位置。

## Monorepo 大致分工

当前仓库的 `packages/` 按交付面和能力边界组织。可以粗略理解为：

| 包组 | 主要职责 |
|------|----------|
| `opencode` | 主运行时、CLI、会话、工具、配置、服务端路由 |
| `app` / `desktop` / `web` / `console` | 各用户界面与交互入口 |
| `sdk` / `ui` / `shared` | 公共类型、组件、共享能力 |
| `plugin` / `extensions` / `function` | 扩展与运行时对接面 |
| `script` / `containers` / `identity` / `enterprise` / `slack` / `storybook` | 构建、集成、部署和周边能力 |

这类组织方式更适合长期演进，因为它允许底层运行时和外层产品面各自发展，而不必强行塞进单一目录模式里。

## 当前主线里最关键的架构选择

### 1. MiMo 基座优先

如果 MiMo 当前主线已经提供能力，龙山灵码优先继承，而不是重写。这样做的直接收益是：

- 长任务运行时保持完整
- 上游能力更容易继续跟进
- SWUST 可以把精力放在中文体验、工程防护和治理层

### 2. 长任务能力放在主路径

记忆、checkpoint、goal、subagent、workflow 位于主任务链路中。这样设计之后：

- 会话恢复不会变成旁路逻辑
- 子智能体能回写任务上下文
- 目标驱动和任务状态可以持续生效

### 3. 工程防护也是运行时能力

Task Gate、Bash Safety、Write Guard、Document Validation 会影响实际执行边界，因此属于运行时能力。

## 面向开发者的阅读顺序

如果你准备继续维护当前主线，推荐先按这个顺序阅读：

1. [主线状态](/mainline-status)
2. [SWUST 优势](/DIFFERENCES)
3. [智能体模式](/features/agents)
4. [持久化记忆](/features/memory)
5. [工作流引擎](/features/workflow)

这条路径更接近当前主线真实的设计中心。
