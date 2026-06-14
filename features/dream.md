# 自我进化

v0.3 把 Dream 和 Distill 从说明型命令推进为可运行的自治任务。两个命令都会复用 `runAutonomyTask()`，启动带 `--goal` 的 `swust-code run`，让主 Agent 完成记忆整合或工作流打包。

## Dream（知识提炼）

```bash
swust-code dream
```

常用选项：

| 选项 | 说明 |
|------|------|
| `--dry-run` | 只展示任务文本，不启动 Agent |
| `--yes`, `-y` | 跳过确认 |
| `--model`, `-m` | 指定 `provider/model` |
| `--agent` | 指定 primary agent |
| `--dir` | 指定项目目录 |

Dream 会启动标题为 `Auto Dream` 的自治 run，目标是把经过验证的持久项目知识整合进 SWUST Code memory。

**任务要求**：
1. 以 memory 文件为工作索引
2. 以原始 trajectory 数据库为事实来源
3. 只用只读 SQLite 和文件系统检查
4. 只写入持久、可验证的信息

## Distill（技能发现）

```bash
swust-code distill
```

Distill 会启动标题为 `Auto Distill` 的自治 run，目标是识别重复工作流，并只创建高置信度缺失的技能、Agent 或命令。

**任务要求**：
1. 回顾最近一个月会话
2. 用 trajectory 数据库核对重复手工流程
3. 先盘点已有 skills、agents、commands
4. 输出紧凑候选清单
5. 只创建确定有价值的缺失资产

## 自动触发

普通会话结束后，core runner 会尝试动态加载 `session/auto-dream.ts`，满足条件时在后台入队对应命令。

| 任务 | 间隔 | 后台命令 |
|------|------|----------|
| Dream | 7 天 | `swust-code dream --yes --dir <cwd>` |
| Distill | 30 天 | `swust-code distill --yes --dir <cwd>` |

触发条件：

- `SWUST_CODE_AUTO_EVOLUTION` 没有设置为 `0` 或 `false`
- 距离上一次同标题会话超过间隔
- 项目已有足够久的历史会话
- 距离上一次 spawn 至少 10 秒

子进程会把 `SWUST_CODE_AUTO_EVOLUTION=0` 写入环境，防止自动进化任务递归触发自身。
