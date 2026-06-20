# Quick Start

SWUST Code is a terminal-native AI coding agent built on MiMo-Code. It is designed for long-running software engineering work: reading and editing code, running commands, using MCP / LSP / plugins, maintaining persistent project memory, and continuing work through goal, compose, subagents, and checkpoints.

## 1. Install

```bash
# One-line install
curl -fsSL https://raw.githubusercontent.com/MakeBlackSheepGreat/swust-code/main/install | bash

# Or install via npm
npm install -g @swust-code/cli
```

Confirm that the CLI is available:

```bash
swust-code --version
```

## 2. First Run

```bash
swust-code
```

The first launch opens the provider setup guide.

| Option | Use When |
|--------|----------|
| MiMo Auto | You want a zero-config free-for-limited-time channel |
| Xiaomi MiMo Platform | You want to sign in with MiMo OAuth |
| Import from Claude Code | You already have Claude Code credentials on this machine |
| Custom Provider | You use an OpenAI-compatible gateway or another model vendor |

Provider and model names are not rebranded. `MiMo Auto`, `Xiaomi MiMo Platform`, `mimo/mimo-auto`, and `xiaomi/mimo-*` remain provider or model IDs.

## 3. Common Provider Environment Variables

You can also connect common providers with environment variables:

```bash
export ANTHROPIC_API_KEY="your-key"
export OPENAI_API_KEY="your-key"
export GOOGLE_API_KEY="your-key"
```

To inspect or log in to providers:

```bash
swust-code providers list
swust-code providers login
swust-code providers login --provider xiaomi
```

## 4. Everyday Commands

| Command | Purpose |
|---------|---------|
| `swust-code` | Start the interactive TUI |
| `swust-code run "explain this repo"` | Run one prompt from the shell |
| `swust-code run --goal "fix type errors" "start"` | Run with an autonomous stop condition |
| `/goal <objective>` | Set a stop condition inside the TUI |
| `/memory <query>` | Search persistent project memory |
| `/dream` | Consolidate durable project knowledge |
| `/distill` | Package repeated workflows into skills, subagents, or commands |
| `/paste-image` | Attach an image from the clipboard |
| `/model`, `/agent`, `/mcp`, `/skill`, `/effort` | Open common TUI controls through aliases |

## 5. Memory And Checkpoints

SWUST Code keeps cross-session memory on the local machine:

```text
~/.local/share/swust-code/memory/
  global/MEMORY.md
  projects/<project-id>/MEMORY.md
  projects/<project-id>/facts/<fact>.md
  sessions/<session-id>/checkpoint.md
  sessions/<session-id>/notes.md
  sessions/<session-id>/tasks/<task-id>/progress.md
```

Memory is searchable through SQLite FTS5 and reconstructed with checkpoint state when a session resumes or approaches the context limit. `/dream` consolidates durable project knowledge, while `/distill` turns repeated work into reusable workflows.

## 6. Configuration

Runtime configuration uses `swust-code.json` or `swust-code.jsonc`:

```jsonc
{
  "model": "anthropic/claude-sonnet-4-6",
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow"
  }
}
```

Common locations:

| Type | Path |
|------|------|
| Global runtime config | `~/.config/swust-code/swust-code.json` |
| Project runtime config | `swust-code.json` in the project root |
| Global TUI config | `~/.config/swust-code/tui.json` |
| Project TUI config | `tui.json` in the project root |

## Next Steps

- [Installation](/en/guide/install)
- [Configuration](/en/guide/config)
- [LLM Providers](/en/guide/providers)
- [Persistent Memory](/en/features/memory)
- [CLI Commands](/en/api/commands)
