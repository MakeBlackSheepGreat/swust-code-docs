# Skills System

Skills are Markdown instruction packages with frontmatter. They inject task-specific workflows, constraints, scripts, and reference files into a conversation.

Current status: skill discovery, permission filtering, the `skill` tool, and dynamic catalogs are wired. v0.4 also adds compose hidden skills: these are visible only to the `compose` agent mode and do not pollute regular agents.

## Create a Skill

Recommended project location:

```markdown
---
name: code-review
description: Review code changes for correctness, style, and risks
---

# Code Review Skill

## Steps
1. Run `git diff`
2. Review each changed file
3. Classify findings as critical / warning / suggestion
4. Return concrete, actionable feedback
```

## Recognized Fields

| Field | Description |
|-------|-------------|
| `name` | Skill name. Required by the legacy path; core v2 can also infer it from the filename |
| `description` | Skill description shown in the available-skills list |
| `slash` | Core v2 field for marking whether the skill may be exposed as a slash entry |

`hidden`, `allowedTools`, `model`, and `paths` appear in type definitions or older docs, but the active loading paths mainly read `name`, `description`, and core v2 `slash`. Do not rely on those fields for permission narrowing, model switching, or file-path-triggered activation.

## Sources

| Runtime path | Sources |
|--------------|---------|
| core v2 | `skill/` and `skills/` under each config directory, plus local paths or HTTP(S) URLs from the config document `skills` array |
| TUI / legacy | `skill/` and `skills/` under config directories; `.claude/skills/**/SKILL.md` and `.agents/skills/**/SKILL.md`; v1 config `skills.paths` and `skills.urls` |

Remote skill sources must expose an `index.json`. Each listed skill must include `SKILL.md` or a same-name `.md` file. Downloaded remote files are cached locally.

## Loading Behavior

Available skills are listed in system context as `<available_skills>`. When a skill is needed, the model calls the `skill` tool with the skill name; the tool returns the skill body, base directory, and a sampled file list.

Skills are filtered by the `skill` permission resource. If an agent denies a skill name, that skill is hidden from the available list and explicit loading is blocked by the permission system.

## Compose Skill Bundle

The `compose` agent loads a MiMo-style bundled skill set:

| Skill | Purpose |
|-------|---------|
| `plan` | Break down goals into executable plans |
| `parallel` | Dispatch parallel work |
| `review` | Review code and plans |
| `verify` | Verify results and reduce risk |
| `merge` | Merge multiple outputs |
| `subagent` | Coordinate subagent roles |
| `tdd` | Drive implementation through tests |

These skills are injected through compose reminders and the `skill` tool catalog only when the active agent is `compose`.
