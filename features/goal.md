# 目标驱动自治

通过 `--goal` 参数设定目标后，运行循环会在 Agent 尝试停止时进入 Goal Gate 检查。v0.3 已把独立 LLM Judge 接入 core runner：它会读取会话转录、工具结果和目标条件，并返回结构化判定。

## 使用方式

```bash
swust-code run --goal "修复所有 TypeScript 类型错误" "开始工作"
```

## 工作流程

1. 用户通过 `--goal` 设定目标
2. Agent 执行普通工具调用
3. Agent 准备停止时触发 Goal Gate
4. runner 组装转录并解析当前模型
5. Goal Judge 使用 `LLM.generateObject()` 生成 `{ ok, impossible, reason }`
6. 未达成时发布 synthetic reminder 并继续
7. 已达成或不可能时清除目标并停止

## Goal Judge

Judge 使用独立系统提示词，要求严格依据代码改动、测试结果、文件状态和工具输出判断目标是否满足。

| 行为 | 当前实现 |
|------|----------|
| 输出结构 | `Verdict` schema：`ok`、`impossible`、`reason` |
| 采样参数 | `temperature: 0`、`maxTokens: 500` |
| 上下文 | 用户、assistant 文本、reasoning、工具成功/失败结果、shell 输出、压缩摘要 |
| 失败策略 | Judge 调用失败时返回未达成并继续，避免误判完成 |

## 重入控制

| 角色 | 最大重入次数 |
|------|------------|
| 主 Agent | 12 次 |

超过上限后目标会被清除，防止无限循环。

## Task Gate

`taskGate()` 仍可检查 non-terminal tasks 并生成继续提醒。当前 core runner 传入的任务列表仍为空数组，后续需要接入真实 `todowrite` 状态。
