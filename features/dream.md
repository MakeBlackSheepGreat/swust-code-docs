# 自我进化

SWUST Code 从你的使用模式中学习，持续改进自身能力。

## Dream（知识提炼）

```bash
swust-code dream
```

当前状态：`dream` CLI 命令、专用 agent prompt 和 7 天间隔判断代码已经存在；自动触发函数目前返回 false，完整自动调度尚未接入会话生命周期。现阶段请手动运行命令。

**做什么**：
1. 扫描最近 7 天的会话轨迹
2. 从 checkpoint.md 和 notes.md 中提取持久知识
3. 在 SQLite 轨迹数据库中验证事实
4. 将验证后的知识写入 MEMORY.md
5. 移除过时和矛盾的条目

**MEMORY.md 结构**：
- `## Rules` — 用户明确声明的项目规则
- `## Architecture decisions` — 设计决策 + 日期 + 理由
- `## Discovered knowledge` — 跨会话发现的持久知识
- `## Patterns` — 重复出现的问题和解决方案
- `## Gotchas` — 容易踩的坑

**约束**：MEMORY.md ≤ 200 行 / ≤ 10KB

## Distill（技能发现）

```bash
swust-code distill
```

当前状态：`distill` CLI 命令、专用 agent prompt 和 30 天间隔判断代码已经存在；CLI 处理器仍是提示型 stub，完整子智能体编排标记为后续阶段。

**做什么**：
1. 分析最近 30 天的工具使用模式
2. 识别重复出现 ≥ 2 次的工作流
3. 评估是否值得打包为技能
4. 生成 SKILL.md 文件到 `.swust-code/skills/`

**打包形式**：
- **Skill** — SKILL.md 声明式技能
- **Agent** — 专用子智能体配置
- **Command** — 参数化的提示模板

## 自动触发机制

| 任务 | 间隔 | 检查条件 |
|------|------|----------|
| Dream | 7 天 | 上次 Dream 会话时间 |
| Distill | 30 天 | 上次 Distill 会话时间 |

前置检查：
- 项目年龄必须超过间隔时间
- 距上次触发 ≥ 10 秒（防抖）

实现进度：
- `session/auto-dream.ts` 已定义间隔、标题和任务文本
- `shouldAutoDream()` 和 `shouldAutoDistill()` 目前都会返回 false
- `dream` 命令会展示记忆整合说明并请求确认
- `distill` 命令会展示工作流打包说明，但仍提示完整编排需要后续实现
