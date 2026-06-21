# Mainline Status

Declared version: `v0.6.0`

Repository: <https://github.com/MakeBlackSheepGreat/swust-code>

## Current Version

v0.6.0 is based on MiMo-Code. Runtime capabilities that already exist in MiMo-Code keep their original implementation, including memory, checkpoints, actor / subagent, `goal`, `compose`, Dream / Distill, MCP, LSP, plugins, and the TUI / Server Runtime.

The SWUST layer mainly adds:

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

## Version Wording

When the docs mention memory, checkpoints, subagents, `goal`, `compose`, Dream / Distill, and related runtime behavior, they refer to the MiMo-Code implementation inherited by the current mainline. SWUST-specific wording is reserved for behavior that SWUST actually adds or changes, such as Task Gate, Bash Safety, Write Guard, Document Validation, and project-level `/subagent` settings.

Provider and model names keep their original names:

- `MiMo Auto`
- Xiaomi MiMo Platform
- `mimo/mimo-auto`
- `xiaomi/mimo-*`

These are provider or model identifiers and remain unchanged in configuration and documentation.

## Next Reading

- [Quick Start](/en/guide/start)
- [SWUST Advantages](/en/DIFFERENCES)
- [Agent Modes](/en/features/agents)
- [Persistent Memory](/en/features/memory)
- [Workflow Engine](/en/features/workflow)
