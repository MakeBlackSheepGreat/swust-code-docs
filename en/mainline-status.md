# Mainline Status

> Updated: 2026-06-20  
> Repository: <https://github.com/MakeBlackSheepGreat/swust-code>  
> Current declared version: v0.5.0

## Current Position

SWUST Code now uses MiMo-Code as its runtime base. The project keeps SWUST branding, Chinese-first UX, and engineering safeguards, but it does not rewrite MiMo-Code capabilities back toward the older OpenCode-style implementation.

Maintenance rules:

| Case | Rule |
|------|------|
| MiMo-Code already provides the capability | Keep the MiMo-Code native implementation |
| MiMo-Code does not provide the capability | Add the SWUST layer with minimal change |
| Provider or model names | Keep upstream service names unchanged |
| Old SWUST Code behavior conflicts with MiMo-Code | Prefer MiMo-Code behavior |

## Capability Boundary

The MiMo-Code base provides:

- terminal TUI, server runtime, web / desktop surfaces
- multi-provider model routing and OpenAI-compatible providers
- LSP, MCP, plugins, custom commands, skills
- persistent memory, checkpoints, context reconstruction
- actor / subagent orchestration and task tracking
- `goal`, `compose`, Dream / Distill, and voice input

The SWUST layer adds:

- 龙山灵码 branding and Chinese localization
- richer TUI sidebar context and getting-started hints
- attention notifications and sound-pack configuration
- Task Gate, Bash Safety, and Write Guard
- Document Validation and cache-stable context layout
- `@path` memory imports and one-fact-per-file fact storage
- `/memory`, `/paste-image`, and common TUI control aliases

## TUI Status

The current mainline keeps the MiMo/OpenTUI terminal experience while carrying over the useful old SWUST Code sidebar organization. The sidebar covers working directory, instruction files, Goal, Task, Todo, LSP, MCP, changed files, context window, token, cost, and cache sections.

The home Logo uses the SWUST Code deep-blue primary color. Sidebar colors stay close to the old SWUST Code reading experience.

## Provider Naming

These names are provider or model IDs and are not part of SWUST branding replacement:

- `MiMo Auto`
- `Xiaomi MiMo Platform`
- `mimo/mimo-auto`
- `xiaomi/mimo-*`

## Validation Status

Before the latest push, the mainline passed TypeScript typecheck for the CLI package and command-related tests. Before a formal release, run the full build, full test suite, release flow, and npm publish validation.

## Documentation Rule

Public documentation should describe stable current capabilities and user-executable paths. Temporary branches, PR state, local build notes, commit hashes, and agent-session process logs should not be added to the docs site.
