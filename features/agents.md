# 智能体模式

v0.4 把 SWUST Code 的运行入口进一步对齐 MiMo Code：`compose`、`goal`、普通主 Agent、后台子 Agent 和系统 Agent 都按“智能体模式”组织。这样做的直接结果是提示词、技能目录、会话切片、任务状态和后台通知都能走同一套运行时。

## 模式总览

| 模式 | 入口 | 用途 |
|------|------|------|
| `main` | 默认会话 | 普通编码、问答、工具调用 |
| `compose` | `--agent compose` 或配置选择 | 规划、并行、评审、合并等 MiMo 风格复合工作流 |
| `goal` | `swust-code run --goal ...` | 目标驱动自治，未完成时继续推进 |
| subagent | `actor` / `subagent` / workflow | 任务拆分、后台执行、结果回传 |
| `checkpoint-writer` | 系统触发 | 写入 `checkpoint.md`、`MEMORY.md`、任务进度摘要 |
| `dream` / `distill` | CLI 或后台周期触发 | 记忆整理与技能沉淀 |

## Compose 智能体

`compose` 模式直接吸收 MiMo Code 的 compose 能力：内置 bundle 中包含 `plan`、`parallel`、`review`、`verify`、`merge`、`subagent`、`tdd` 等技能。运行时会把这些技能作为 compose 的隐藏技能目录注入，普通 Agent 的可用技能列表不会被污染。

关键行为：

- compose 专用 system reminder 会在 `agent === "compose"` 时注入。
- hidden compose skills 只对 compose 模式可见。
- `skill` 工具会生成动态 catalog，帮助模型按任务选择对应技能。
- 复合任务优先使用规划、并行执行、复核和合并的闭环。

## Goal 智能体

v0.4 把 Goal 从“命令参数触发的指令”改为一种智能体模式。`swust-code run --goal "目标"` 在没有显式 `--agent` 时默认路由到 `goal` Agent；如果用户指定了 `--agent`，显式 Agent 优先。

Goal 模式保留 v0.3 的 LLM Judge 和 Goal Gate，同时新增独立 prompt 与 reminder 注入。这样自治目标、当前上下文和继续工作提醒都能绑定到同一个 Agent 身份，避免混在默认主 Agent 的普通对话提示里。

## Actor 运行时

Actor Spawn 已按 MiMo 风格重构：

- subagent 使用父会话，但通过 `agentID` 写入独立消息切片。
- peer actor 仍使用 child session 做隔离。
- 后台 actor 返回可等待的 outcome，前台调用会等待完成，后台调用可通过 wait/status/cancel 查询。
- `preStop` 和 `postStop` hook 可触发 ReAct 重入。
- 任务绑定会自动 start、done 或 block，并根据 return header 做结果归因。
- Inbox、Actor Registry、Task Registry 持久化，后台子 Agent 的状态不会只停留在内存里。

## Checkpoint Writer

v0.4 补齐了 MiMo 风格 checkpoint writer 的真实启动链：

- 上下文溢出时优先插入 checkpoint boundary，再回退到传统 compaction。
- writer 以后台子 Agent 运行，并使用 child session 隔离自身消息。
- `parentSessionID` 会透传给 checkpoint splitover 插件，确保写入父会话的 `checkpoint.md` 和 `MEMORY.md`。
- 同一会话同时只运行一个 writer；新请求进入 1-slot pending queue，新范围覆盖旧 pending。
- writer 完成后推进 `last_checkpoint_message_id`，后续 rebuild 只加载 checkpoint 和保留 tail。

## 何时使用

| 场景 | 推荐模式 |
|------|----------|
| 一次性修复或问答 | `main` |
| 明确目标、希望模型持续推进 | `goal` |
| 大任务需要拆解、并行、复核 | `compose` |
| 主 Agent 需要派发独立调查或实现任务 | `actor run` / `actor spawn` |
| 长会话接近上下文上限 | 自动 checkpoint writer |

