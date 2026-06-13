# 工作流引擎

工作流模块用于承载脚本化多 Agent 编排的运行时骨架。

当前状态：`packages/opencode/src/workflow/runtime.ts` 已定义工作流运行记录、状态查询、取消接口、metadata 解析、journal 数据结构和并发/生命周期常量。实际脚本执行、host 函数注入、子 Agent 派生、QuickJS 沙箱和崩溃恢复恢复执行仍是后续增强；当前 `start()` 会解析 `meta` 后立即把 run 标记为 `completed`。

## 运行模型

运行时当前维护以下状态：

| 字段 | 说明 |
|------|------|
| `runID` | 工作流运行 ID |
| `sessionID` | 关联会话 |
| `status` | `pending`、`running`、`completed`、`failed`、`cancelled` |
| `name` | 从脚本 `meta.name` 解析 |
| `currentPhase` | 从 `meta.phases[0].title` 初始化 |
| `agentCount` 等计数 | 已定义字段，完整计数更新待脚本执行接入 |

## Metadata

当前实现会从脚本中解析简单的 `export const meta = { ... }`：

```javascript
export const meta = {
  name: 'my-workflow',
  description: '自定义工作流',
  phases: [{ title: 'Phase 1' }],
}
```

解析成功后，`name` 和首个 phase 会写入运行记录。

## 预留 Host 函数

类型层已经定义以下 host 函数接口：

| 函数 | 计划用途 |
|------|----------|
| `agent(prompt, opts?)` | 派生子 Agent 执行任务 |
| `parallel(thunks)` | 并行执行多个任务 |
| `pipeline(items, ...stages)` | 流水线处理 |
| `phase(title)` | 标记阶段 |
| `log(message)` | 写入日志 |
| `workflow(name, args?)` | 调用其他工作流 |

这些函数目前还没有被注入到可执行沙箱中。

## Journal

`WorkflowJournal` 当前是内存结构，支持追加 `phase`、`agent_start`、`agent_complete`、`agent_fail`、`log`、`error` 事件，并能读取最后一个 phase。

持久化 JSONL、脚本 hash 校验和断点恢复仍待接入。
