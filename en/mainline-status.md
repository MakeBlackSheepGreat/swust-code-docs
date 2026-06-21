# Mainline Status

Declared version: `v0.6.0`

Repository: <https://github.com/MakeBlackSheepGreat/swust-code>

## Current Version

v0.6.0 is based on MiMo-Code and includes long-task runtime capabilities such as memory, checkpoints, actor / subagent, `goal`, `compose`, Dream / Distill, MCP, LSP, plugins, and the TUI / Server Runtime.

This version adds the following SWUST-side work:

- Chinese-first TUI wording and information layout
- richer sidebar context
- Task Gate, Bash Safety, and Write Guard
- Document Validation and cache-stable context layout
- `@path` memory imports and one-fact-per-file fact storage
- `/memory`, `/paste-image`, `/subagent`, and `/subagents`

## Fit

| Workload | Status |
|----------|--------|
| multi-step coding work inside real repositories | good fit |
| long tasks that need resume behavior | good fit |
| subagent delegation, review, and parallel execution | good fit |
| durable project knowledge and memory maintenance | good fit |
| one-shot conceptual questions | not the main target |

## Next Reading

- [Quick Start](/en/guide/start)
- [SWUST Advantages](/en/DIFFERENCES)
- [Agent Modes](/en/features/agents)
- [Persistent Memory](/en/features/memory)
- [Workflow Engine](/en/features/workflow)
