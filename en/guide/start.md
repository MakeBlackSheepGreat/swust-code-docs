# Quick Start

SWUST Code is a terminal AI coding tool built on MiMo-Code for repository work that continues across files, stages, and sessions.

## What It Fits Best

SWUST Code is usually a strong fit when the task:

- spans multiple files or phases
- benefits from delegated subagent work
- needs durable project rules or architectural memory
- must resume later without rebuilding context from scratch

## 1. Install

```bash
# One-line install
curl -fsSL https://raw.githubusercontent.com/MakeBlackSheepGreat/swust-code/main/install | bash

# Or install via npm
npm install -g @swust-code/cli
```

Confirm the CLI is available:

```bash
swust-code --version
```

## 2. First Launch

```bash
swust-code
```

The first launch opens provider setup. Common options are:

| Option | Use when |
|--------|----------|
| `MiMo Auto` | You want the fastest zero-config start |
| `Xiaomi MiMo Platform` | You want to sign in with MiMo OAuth |
| `Import from Claude Code` | Claude Code credentials already exist on this machine |
| `Custom Provider` | You use an OpenAI-compatible gateway or another provider |

Provider and model names keep their original naming. `MiMo Auto`, `Xiaomi MiMo Platform`, `mimo/mimo-auto`, and `xiaomi/mimo-*` remain provider or model identifiers.

If you prefer to manage providers from the terminal:

```bash
swust-code providers list
swust-code providers login
swust-code providers import
```

## 3. A Recommended First Path

For a first project session, this sequence tends to work well:

1. start `swust-code` in the project root
2. begin with the default primary agent, then switch to `plan`, `compose`, or `goal` only when needed
3. use `/goal` or `swust-code run --goal ...` when the task has a clear stop condition
4. use `compose` or subagents for decomposition, review, or parallel work
5. use `/dream` or `/distill` at the end of a phase to retain knowledge and package repeated work

This path covers task execution, resume behavior, and knowledge consolidation in one workflow.

## 4. Everyday Commands

| Command | Purpose |
|---------|---------|
| `swust-code` | Start the interactive TUI |
| `swust-code run "explain this repo"` | Run one prompt from the shell |
| `swust-code run --goal "fix type errors" "start"` | Autonomous run with a stop condition |
| `/goal <objective>` | Set a stop condition for the current session |
| `/memory <query>` | Search persistent project memory |
| `/subagent`, `/subagents` | Configure model, reasoning variant, and max steps for visible subagents |
| `/dream` | Consolidate recent work into durable knowledge |
| `/distill` | Turn repeated workflows into skills, commands, subagents, or workflows |
| `/paste-image` | Attach an image from the clipboard |
| `/model`, `/agent`, `/mcp`, `/skill`, `/effort` | Open common selectors and control surfaces |

## 5. Config Files And Project Directories

SWUST Code uses both config files and project-local directories:

| Location | Purpose |
|----------|---------|
| `~/.config/swust-code/swust-code.json` | global runtime config |
| `swust-code.json` in the project root | project runtime config |
| `~/.config/swust-code/tui.json` | global TUI config |
| `tui.json` in the project root | project TUI config |
| `.swust-code/` inside the project | project-level agents, commands, skills, workflows, and plugins |

Common project-local directories include:

- `.swust-code/agents/`
- `.swust-code/commands/`
- `.swust-code/skills/`
- `.swust-code/workflows/`
- `.swust-code/plugins/`

If you only need provider, model, permission, or agent configuration, start with `swust-code.json`. If you want repository-owned commands, skills, or workflows, use `.swust-code/`.

## 6. Memory, Checkpoints, And Resume

SWUST Code maintains durable local memory:

```text
~/.local/share/swust-code/memory/
  global/MEMORY.md
  projects/<project-id>/MEMORY.md
  projects/<project-id>/facts/<fact>.md
  sessions/<session-id>/checkpoint.md
  sessions/<session-id>/notes.md
  sessions/<session-id>/tasks/<task-id>/progress.md
```

This structure exists to support three things:

- preserving durable project rules and facts
- recovering long sessions near the context limit
- letting subagent work flow back into the primary task chain

If what you care about is whether the agent can continue later without relearning the project, this is the part that matters.

## Next Reading

- [Installation](/en/guide/install)
- [Configuration](/en/guide/config)
- [LLM Providers](/en/guide/providers)
- [Agent Modes](/en/features/agents)
- [Persistent Memory](/en/features/memory)
- [Workflow Engine](/en/features/workflow)
