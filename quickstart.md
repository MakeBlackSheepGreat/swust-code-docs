# SWUST Code Quick Start

## Installation

```bash
npm install -g swust-code
```

## First Run

```bash
# Start interactive TUI
swust-code

# Run a single command
swust-code run "explain this project"

# Set an autonomous goal
swust-code run --goal "fix all TypeScript errors" "start working"
```

## Configuration

Create `swust-code.jsonc` in your project root, or place it under `.swust-code/swust-code.jsonc`:

```json
{
  "model": "anthropic/claude-sonnet-4-6",
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow"
  }
}
```

## Memory System

SWUST Code remembers project knowledge across sessions:

```bash
# Memory files are stored at:
# ~/.local/share/swust-code/memory/projects/<id>/MEMORY.md

# The agent automatically:
# - Indexes memory files for full-text search
# - Injects relevant context into conversations
# - Supports manual Dream and Distill entry points
```

## Key Commands

| Command | Description |
|---------|-------------|
| `swust-code` | Start interactive TUI |
| `swust-code run "msg"` | Run with a message |
| `swust-code run --goal "cond" "msg"` | Goal/Gate re-entry mode; Judge integration is still pending |
| `swust-code dream` | Start the memory consolidation command flow |
| `swust-code distill` | Start the workflow packaging command flow |
| `swust-code mcp list` | List MCP servers |
| `swust-code providers list` | List AI provider credentials |
| `swust-code providers import` | Import credentials from MiMo-Code, Claude Code, or env vars |

## Skills

Create custom skills in `.swust-code/skill/<name>.md` or `.swust-code/skills/<name>/SKILL.md`:

```markdown
---
name: my-skill
description: What this skill does
---

# Instructions for the skill...
```

## Memory Files

Organize knowledge in memory directories:

```
~/.local/share/swust-code/memory/
  global/MEMORY.md              # Cross-project preferences
  projects/<hash>/MEMORY.md     # Project-specific knowledge
  sessions/<id>/checkpoint.md   # Session checkpoints
```
