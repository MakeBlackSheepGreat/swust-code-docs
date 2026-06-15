# 技能系统

技能是带 frontmatter 的 Markdown 指令包，用于把特定任务的流程、约束、脚本和参考文件按需注入会话。

当前状态：技能发现、权限过滤、`skill` 工具加载和动态 catalog 已经接入。v0.4 额外加入了 compose hidden skills：这些技能只在 `compose` Agent 模式下出现，普通 Agent 不会看到。

## 创建技能

推荐放在项目 `.swust-code/skills/<name>/SKILL.md`：

```markdown
---
name: code-review
description: 审查代码变更的正确性、风格和潜在问题
---

# 代码审查技能

## 步骤
1. 运行 `git diff` 查看变更
2. 逐文件分析 diff
3. 按严重程度分类：critical / warning / suggestion
4. 提供具体的、可操作的反馈

## 输出格式
### Critical Issues
- [file:line] 问题描述
```

## 当前识别字段

| 字段 | 说明 |
|------|------|
| `name` | 技能名称。旧链路要求必填；core v2 也可从文件名推导 |
| `description` | 技能描述，会出现在可用技能列表中，帮助模型判断何时加载 |
| `slash` | core v2 frontmatter 字段，用于标记技能是否可作为 slash 入口暴露 |

`hidden`、`allowedTools`、`model`、`paths` 在类型定义或旧文档中出现过，但当前加载链路主要读取 `name`、`description` 和 core v2 的 `slash`。不要依赖这些字段完成权限收敛、模型切换或文件路径自动激活。

## 加载来源

运行时有两套技能发现路径：

| 链路 | 来源 |
|------|------|
| core v2 | 每个配置目录下的 `skill/`、`skills/`，以及配置文档 `skills` 数组里的本地路径或 HTTP(S) URL |
| TUI/旧链路 | 配置目录下的 `skill/`、`skills/`；用户或项目中的 `.claude/skills/**/SKILL.md`、`.agents/skills/**/SKILL.md`；v1 配置 `skills.paths` 与 `skills.urls` |

远端技能源需要提供 `index.json`，每个技能至少包含 `SKILL.md` 或同名 `.md` 文件。下载后的远端文件会进入本地 cache。

## 加载行为

可用技能会进入 system context 的 `<available_skills>` 列表。模型需要使用技能时调用 `skill` 工具并传入技能名；工具会返回技能正文、技能目录和采样文件列表。

技能权限通过 `skill` 资源名过滤。如果 agent 权限规则拒绝某个技能，它不会出现在该 agent 的可用列表中，显式加载也会被权限系统拦截。

## Compose 技能 bundle

`compose` Agent 会加载 MiMo 风格的内置技能 bundle，用于处理复杂任务：

| 技能 | 用途 |
|------|------|
| `plan` | 拆解目标、形成执行计划 |
| `parallel` | 并行派发子任务 |
| `review` | 代码和方案复核 |
| `verify` | 验证结果、收敛风险 |
| `merge` | 汇总多路输出 |
| `subagent` | 组织子 Agent 角色 |
| `tdd` | 测试驱动实现 |

这些技能不会进入普通 `<available_skills>`，但会通过 compose reminder 和 `skill` 工具 catalog 提供给 compose 模式。
