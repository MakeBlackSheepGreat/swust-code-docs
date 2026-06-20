# Mainline Status

> Updated: 2026-06-20  
> Code repository: <https://github.com/MakeBlackSheepGreat/swust-code>  
> Mainline PR: [#1](https://github.com/MakeBlackSheepGreat/swust-code/pull/1)

## Current State

The MiMo-Code based SWUST Code migration is ready for mainline review. The old `main` branch and the MiMo-based `mimo-rebase` branch do not share a merge base, so the mainline update uses a bridge PR branch.

| Item | State |
|------|-------|
| Base branch | `main` |
| Migration branch | `mimo-rebase` |
| PR branch | `pr/mimo-rebase-to-main` |
| PR status | Open / Mergeable |
| Latest migration commit | `520db45 docs: rewrite swust code readme` |
| Internal package version | `0.1.1` |
| Current local preview build version | `0.0.0-swust-code-rebrand-202606200248` |

The bridge PR branch resolves to the exact same file tree as `swust-code/mimo-rebase`. Its first parent is the old `main`, and its second parent is `mimo-rebase`, allowing GitHub to create and merge the PR while preserving the migration branch history.

## Completed

### MiMo-Code Base Migration

- Switched the project base to the MiMo-Code fork.
- Kept MiMo-Code native capabilities: providers, TUI, LSP, MCP, plugins, persistent memory, checkpoints, actors/subagents, tasks, goal, Compose, Dream/Distill, and voice.
- Rebranded packages, CLI, environment variables, config paths, documentation links, and UI copy to SWUST Code / 龙山灵码.
- Preserved provider names: `MiMo Auto`, `Xiaomi MiMo Platform`, `mimo/mimo-auto`, and `xiaomi/mimo-*` remain provider/model names.

### SWUST Layer

- Task Gate for unfinished-work checks before agent stop.
- Bash Safety for risky shell command analysis.
- Cache-Stable Prefix for provider cache hit improvement.
- `@path` memory imports and one-fact-per-file fact store.
- Memory and task progress write guards.
- Document validation for spec-driven files.

### TUI And Docs

- The SWUST sidebar experience is migrated: working directory, instruction files, goal, task, todo, LSP, MCP, changed files, context window, token, cost, and cache sections.
- `TuiPathsProvider` is wired into the TUI app runtime.
- Getting-started hints, path display, and Chinese i18n are present.
- Attention notifications and sound-pack configuration are wired.
- README / README.zh were rewritten in the old SWUST Code style while correcting the base relationship to MiMo-Code.

## Validation

- `bun turbo typecheck` before pushing the migration branch: 12/12 tasks successful.
- `bun turbo typecheck` before pushing the PR branch: 12/12 tasks successful.
- GitHub PR [#1](https://github.com/MakeBlackSheepGreat/swust-code/pull/1) is currently `MERGEABLE`.
- Local note: Bun is `1.3.14`; the repository declares `bun@1.3.11`.

## Follow-up

- After PR #1 is merged into `main`, verify automatic deployment, release, and npm publish flows.
- For a formal release build, use a release channel so the build version resolves to `packages/opencode/package.json` version `0.1.1` instead of a branch preview version.
- Continue syncing provider/config documentation from the new repository's `packages/web/src/content/docs`.

