# Mainline Status

> Current declared version: v0.6.0
> Repository: <https://github.com/MakeBlackSheepGreat/swust-code>

## What The Current Mainline Is

The current SWUST Code mainline uses MiMo-Code as its runtime base. This is an implementation rule, not just branding language:

- if MiMo-Code already provides the runtime capability, the mainline keeps the MiMo implementation
- SWUST-specific work is added as a product layer where possible instead of rewriting the base back toward older OpenCode-era behavior
- provider, model, and service names stay unchanged

The mainline should therefore be understood as **a SWUST product layer on top of the MiMo-Code base**, not a regression to the historical pre-MiMo stack.

## What It Inherits From MiMo-Code

The current mainline inherits MiMo-Code's core runtime capabilities:

- terminal TUI, server runtime, and web / desktop surfaces
- multi-provider model routing and OpenAI-compatible integrations
- LSP, MCP, plugins, custom commands, and skills
- persistent memory, checkpoints, and context reconstruction
- actor / subagent orchestration and task tracking
- `goal`, `compose`, Dream / Distill, and voice input

In public documentation, these should be described as inherited MiMo capabilities, not relabeled as SWUST inventions.

## What The SWUST Layer Adds

On top of the MiMo base, the current mainline strengthens the product around real engineering use:

- SWUST branding, Chinese localization, and Chinese-first information flow
- richer TUI sidebar context and getting-started guidance
- attention notifications and sound-pack configuration
- Task Gate, Bash Safety, and Write Guard
- Document Validation and cache-stable context layout
- `@path` memory imports and one-fact-per-file fact storage
- `/memory`, `/paste-image`, and familiar control aliases
- `/subagent` / `/subagents` for project-level visible-subagent customization

The point is not to accumulate feature labels. The point is to make the mainline more usable for long-running engineering work.

## Capability Boundary

The current mainline is primarily designed for:

| Workload | Fit |
|----------|-----|
| multi-step coding work inside real repositories | strong |
| long tasks that must resume and continue | strong |
| subagent delegation, review, and parallel work | strong |
| durable project knowledge accumulation | strong |
| short one-shot chat or demo prompting | not the primary target |

That means the mainline's value is mostly in continuity, engineering constraint awareness, and recovery behavior rather than single-turn speed.

## TUI And Daily Use

The current mainline keeps MiMo's terminal runtime model while preserving several SWUST choices that matter in daily use:

- a deep-blue SWUST visual identity on the home surface
- sidebar organization and density closer to the stronger parts of earlier SWUST builds
- Chinese-first wording for key commands, prompts, and panels
- per-project model, reasoning-variant, and step overrides for visible subagents

These changes are meant to reduce friction during real terminal work, not just change the skin.

## Provider Naming

The following names are provider or model identifiers and are intentionally not rebranded:

- `MiMo Auto`
- `Xiaomi MiMo Platform`
- `mimo/mimo-auto`
- `xiaomi/mimo-*`

Documentation, UI, and configuration should keep these original names.

## Ongoing Maintenance Rule

As the mainline continues to evolve, the recommended decision order is:

1. check whether MiMo current mainline already provides the capability
2. if it does, inherit it instead of rewriting it
3. if it does not, add the SWUST layer
4. if an older SWUST branch had it but MiMo current mainline does not, decide whether it still belongs in the current mainline

That is the stable documentation rule for the current public mainline.
