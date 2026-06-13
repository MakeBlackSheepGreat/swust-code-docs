# 目标驱动自治

通过 `--goal` 参数设定目标，让运行循环在 agent 尝试停止时检查目标状态。当前代码已经有 Goal Store、Goal Gate 和 12 次重入上限；独立 LLM Judge 的完整接入仍在进行中。

## 使用方式

```bash
swust-code run --goal "修复所有 TypeScript 类型错误" "开始工作"
```

## 工作流程

1. 用户设定 goal（如 "修复所有 lint 错误"）
2. Agent 开始工作，执行工具调用
3. 当 Agent 想要停止时，**Goal Gate** 触发
4. Goal Gate 调用评估函数判断目标状态
5. 如果目标未达成：注入合成消息，Agent 继续工作
6. 如果目标达成或不可能：正常停止

## Goal Judge

目标设计中包含独立的 LLM 评估器，接口返回：

- `{ ok: boolean, impossible?: boolean, reason: string }`
- `ok=true` 时清除目标并停止
- `impossible=true` 时清除目标并停止
- 其他情况会生成 `<system-reminder>` 提醒继续工作

当前核心 runner 里评估函数仍是占位实现，返回 `Judge not yet integrated`。因此 `--goal` 已经暴露为 CLI 参数，但自动判定质量还取决于后续 Judge 接入。

## 重入控制

| 角色 | 最大重入次数 |
|------|------------|
| 主 Agent | 12 次 |

超过上限后强制停止，防止无限循环。

## Task Gate

二级停止条件：`taskGate()` 能检查 non-terminal tasks。如果存在未完成任务，会生成提醒并强制继续。当前 runner 传入的任务列表仍为空数组，后续需要接入真实 todowrite 状态。
