# 技能开发

技能是 `SKILL.md` 或带 frontmatter 的 `.md` 文件。运行时会发现技能、把技能摘要放进可用列表，并在模型调用 `skill` 工具时加载完整内容。

## 创建技能

项目内推荐路径：

```text
.swust-code/skills/my-skill/SKILL.md
```

示例：

```markdown
---
name: my-skill
description: 技能描述，说明何时应该使用它
---

# 技能标题

## 使用场景

当用户需要处理某类任务时使用此技能。

## 步骤
1. 第一步
2. 第二步

## 输出格式

期望的输出格式。
```

## Frontmatter 字段

| 字段 | 当前状态 |
|------|----------|
| `name` | 旧链路要求必填；core v2 可从文件名推导 |
| `description` | 当前会进入可用技能列表，建议填写 |
| `slash` | core v2 识别，用于 slash 暴露标记 |
| `hidden` | 类型里有预留，当前主加载链路不作为隐藏控制 |
| `allowedTools` | 类型里有预留，当前权限仍通过 agent 的 `permission` 规则控制 |
| `model` | 类型里有预留，当前不会自动切换模型 |
| `paths` | 类型里有预留，当前不会自动完成路径条件激活 |

## 来源与注册

默认扫描：

- 配置目录下的 `skill/` 和 `skills/`
- 项目或用户的 `.claude/skills/**/SKILL.md`
- 项目或用户的 `.agents/skills/**/SKILL.md`

额外来源：

```json
{
  "skills": {
    "paths": [".swust-code/skills", "/absolute/path/to/skills"],
    "urls": ["https://example.com/.well-known/skills/"]
  }
}
```

上面的对象形式是当前 CLI/TUI 使用的 v1 配置字段。core v2 配置层也支持 `skills` 字符串数组，并会把本地路径或 HTTP(S) URL 转换为技能来源。

## 测试技能

1. 创建 `SKILL.md`
2. 启动 SWUST Code
3. 查看可用技能列表或使用 `/skill`
4. 让模型调用 `skill` 工具加载该技能
5. 如果技能不可见，检查 `name`、`description`、扫描路径和 `skill` 权限规则
