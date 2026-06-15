# 工作流引擎

工作流运行时已经能执行脚本，并通过显式 host 函数完成多 Agent 编排。当前后端是受限 host-function runner，QuickJS 仍保留为未来可替换的执行边界。v0.4 后，`agent()` 走 MiMo 风格 ActorSpawn，并等待 actor outcome 后再写入 journal。

## 运行模型

`Workflow.Service` 当前提供：

| 方法 | 说明 |
|------|------|
| `start(input)` | 启动工作流，立即返回 `running` 状态 |
| `getStatus(runID)` | 查询运行状态 |
| `cancel(runID)` | 通过 `AbortController` 取消 |
| `getJournal(runID)` | 读取内存 journal |

运行状态包括 `pending`、`running`、`completed`、`failed` 和 `cancelled`。脚本抛错会标记为 `failed`，取消会标记为 `cancelled`。

## 脚本示例

```javascript
export const meta = {
  name: 'my-workflow',
  description: '自定义工作流',
  phases: [{ title: 'Plan' }],
}

phase('Plan')
log('planning')

const result = await agent('summarize the plan', {
  label: 'planner',
  phase: 'Plan',
})

return { ok: true, text: result.text }
```

运行时会解析 `meta`，记录 `name` 和阶段，并将 host 函数注入脚本作用域。

## Host 函数

| 函数 | 当前行为 |
|------|----------|
| `agent(prompt, opts?)` | 通过 Actor Spawn 派生 ephemeral subagent，等待 outcome，记录 agent 计数和结果 |
| `parallel(thunks)` | 并行执行任务；agent 并发受 `maxConcurrentAgents` 限制 |
| `pipeline(items, ...stages)` | 按 stage 处理 item 数组 |
| `phase(title)` | 更新当前阶段并写入 journal |
| `log(message)` | 写入 journal |
| `workflow(name, args?)` | 调用内置工作流，带最大深度 8 和环检测 |

脚本不能使用 `import`、`export` 之外的模块加载、`process`、`Bun`、`Deno`、`fetch`、`eval`、`Function` 等宿主全局。

## Journal 与恢复

工作流会同时维护内存 journal 和磁盘 JSONL：

| 文件 | 作用 |
|------|------|
| `<data>/workflow/<runID>.jsonl` | 记录 phase、log、agent result、error |
| `<data>/workflow/<runID>.js` | 保存脚本内容，用于变更检测 |

agent 调用使用 `sha256(prompt + agentType + model + schema + phase + occurrence)` 生成确定性 key。恢复时会重放已有结果；脚本内容变化会清空旧 journal，避免复用过期结果。

## 内置工作流

内置注册表当前包含 `deep-research`，脚本定义了 Plan、Search、Extract、Group、Crosscheck、Report 六个阶段。`workflow("deep-research", args)` 可从其他脚本中调用。
