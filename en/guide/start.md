# Quick Start

SWUST Code is a terminal-native AI coding agent with persistent memory and self-improvement capabilities.

## Install

```bash
npm install -g @swust-code/cli
```

## First Run

```bash
swust-code
```

The first launch guides you through configuration automatically. You can use MiMo Auto, Xiaomi MiMo Platform login, Claude Code auth import, or any OpenAI-compatible provider.

## Configure API Key

```bash
export ANTHROPIC_API_KEY="your-key"
# or
export OPENAI_API_KEY="your-key"
```

## Basic Usage

```bash
# Interactive mode
swust-code

# Single run
swust-code run "explain this project"

# Autonomous mode
swust-code run --goal "fix all TypeScript errors" "start working"

# Knowledge consolidation
swust-code dream

# Skill discovery
swust-code distill
```

`dream` and `distill` launch autonomous `swust-code run --goal` sessions. After normal sessions finish, the system also checks 7-day Dream and 30-day Distill intervals for background triggering. Set `SWUST_CODE_AUTO_EVOLUTION=0` to disable auto-evolution.

## Memory System

SWUST Code stores persistent memory under `~/.local/share/swust-code/memory/`:

- `global/MEMORY.md` for cross-project preferences
- `projects/<id>/MEMORY.md` for project knowledge
- `sessions/<id>/checkpoint.md` for session checkpoints

The agent indexes these files automatically and retrieves relevant knowledge during conversations. Use `dream` to consolidate project memory when needed.

## Next Steps

- [Installation](/en/guide/install) — Detailed installation methods
- [Configuration](/en/guide/config) — Configuration file reference
- [LLM Providers](/en/guide/providers) — Supported models
- [Persistent Memory](/en/features/memory) — Memory system deep dive
