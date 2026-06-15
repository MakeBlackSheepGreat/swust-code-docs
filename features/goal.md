# 目标驱动自治

通过 `--goal` 参数设定目标后，运行循环会在 Agent 尝试停止时进入 Goal Gate 检查。v0.4 起，Goal 已经成为独立 Agent 模式：没有显式 `--agent` 时，`swust-code run --goal ...` 会路由到 `goal` Agent，并注入 goal 专用 prompt 与 reminder。

## 使用方式

```bash
swust-code run --goal "修复所有 TypeScript 类型错误" "开始工作"
```

## 工作流程

1. 用户通过 `--goal` 设定目标。
2. CLI 在未显式指定 `--agent` 时选择 `goal` Agent。
3. Goal Agent 执行普通工具调用。
4. Agent 准备停止时触发 Goal Gate。
5. runner 组装转录并解析当前模型。
6. Goal Judge 使用 `LLM.generateObject()` 生成 `{ ok, impossible, reason }`。
7. 未达成时发布 synthetic reminder 并继续。
8. 已达成或不可能时清除目标并停止。

## Goal Judge

Judge 使用独立系统提示词，要求严格依据代码改动、测试结果、文件状态和工具输出判断目标是否满足。

| 行为 | 当前实现 |
|------|----------|
| 输出结构 | `Verdict` schema：`ok`、`impossible`、`reason` |
| 采样参数 | `temperature: 0`、`maxTokens: 500` |
| 上下文 | 用户、assistant 文本、reasoning、工具成功/失败结果、shell 输出、压缩摘要 |
| 失败策略 | Judge 调用失败时返回未达成并继续，避免误判完成 |

## Agent 路由

| 命令 | 结果 |
|------|------|
| `swust-code run --goal "修复类型错误" "开始"` | 使用 `goal` Agent |
| `swust-code run --goal "修复类型错误" --agent build "开始"` | 使用显式 `build` Agent |
| `swust-code run "普通问题"` | 使用默认 Agent |

## 重入控制

| 角色 | 最大重入次数 |
|------|------------|
| 主 Agent | 12 次 |

超过上限后目标会被清除，防止无限循环。

## Task Gate

`taskGate()` 会检查未完成任务并生成继续提醒。v0.4 同步补齐了 Task Registry、Actor 任务绑定和 subagent completion gate：任务型子 Agent 会自动 start，完成时 done，失败或 blocked 时 block。
