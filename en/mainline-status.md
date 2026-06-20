# Project Status

> Updated: 2026-06-20  
> Repository: <https://github.com/MakeBlackSheepGreat/swust-code>  
> Current version: v0.5.0

## Current Position

SWUST Code now uses MiMo-Code as its mainline base. The project keeps SWUST branding, Chinese-first experience, and engineering enhancements while relying on MiMo-Code native runtime capabilities.

## Mainline Capabilities

- MiMo-Code native capabilities: persistent memory, checkpoints, actor/subagent orchestration, tasks, goal, Compose, Dream/Distill, voice input, TUI, LSP, MCP, and plugins.
- SWUST enhancements: Task Gate, Bash Safety, Cache-Stable Prefix, `@path` memory imports, Fact Store, Write Guard, and Document Validation.
- Branding and paths: the CLI is `swust-code`, project config lives under `.swust-code/`, and environment variables use the `SWUST_CODE_*` prefix.
- Provider names stay unchanged: `MiMo Auto`, Xiaomi MiMo Platform, `mimo/mimo-auto`, and `xiaomi/mimo-*` remain provider or model names.

## TUI Status

The current mainline includes the SWUST sidebar experience: working directory, instruction files, Goal, Task, Todo, LSP, MCP, changed files, context window, token, cost, and cache sections. Getting-started hints, path display, Chinese i18n, attention notifications, and sound-pack configuration are also wired in.

## Validation Status

The current mainline passed TypeScript typecheck before push. Before a formal release, run the full test, build, release, and npm publish validation flow.

## Maintenance Rules

- If MiMo-Code already provides a capability, prefer the MiMo-Code implementation.
- Only migrate old SWUST Code / OpenCode behavior when MiMo-Code does not provide it.
- Documentation should describe stable current behavior, not temporary branches, commit hashes, or local build metadata.
