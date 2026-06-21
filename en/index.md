---
layout: home

hero:
  name: SWUST Code
  text: "龙山灵码"
  tagline: "A terminal AI coding tool based on MiMo-Code. The current mainline inherits MiMo-Code memory, checkpoints, subagents, goal, compose, MCP, LSP, and plugins, with added Chinese TUI work, engineering safeguards, and project-level subagent settings."
  actions:
    - theme: brand
      text: Quick Start
      link: /en/guide/start
    - theme: alt
      text: Mainline Status
      link: /en/mainline-status
    - theme: alt
      text: SWUST Advantages
      link: /en/DIFFERENCES

features:
  - title: MiMo-Code Base
    details: "The current mainline inherits MiMo-Code runtime behavior. If MiMo already provides a feature, the MiMo implementation remains the default."
    link: /en/mainline-status
  - title: Memory And Checkpoints
    details: "MEMORY.md, facts, checkpoint.md, and task progress store project facts, session state, and task progress."
    link: /en/features/memory
  - title: Multi-Agent Runtime
    details: "build, plan, compose, goal, and subagents are used for analysis, execution, orchestration, and verification."
    link: /en/features/agents
  - title: Engineering Safeguards
    details: "Task Gate, Bash Safety, Write Guard, and Document Validation handle premature stops, risky commands, bad writes, and document-structure errors."
    link: /en/features/security
  - title: Workflow And Consolidation
    details: "workflow is used for resumable multi-stage work; dream and distill consolidate project knowledge and repeated processes."
    link: /en/features/workflow
  - title: Chinese TUI
    details: "Chinese command text, sidebar information, and theme configuration are tuned for daily terminal work."
    link: /en/features/tui
---

## Start Here

| Goal | Page |
|------|------|
| Install and complete the first launch | [Quick Start](/en/guide/start) |
| Check what the current mainline is based on | [Mainline Status](/en/mainline-status) |
| Understand what SWUST adds beyond MiMo | [SWUST Advantages](/en/DIFFERENCES) |
| Understand agents, subagents, goal, and compose | [Agent Modes](/en/features/agents) |
| Understand memory and checkpoint recovery | [Persistent Memory](/en/features/memory) |
| Read CLI and config details | [CLI Commands](/en/api/commands), [Config Schema](/en/api/config-schema) |

## Basic Facts

| Item | Current value |
|------|---------------|
| Chinese name | 龙山灵码 |
| English name | SWUST Code |
| CLI command | `swust-code` |
| Declared version | `v0.6.0` |
| Runtime base | MiMo-Code |
| Project directory | `.swust-code/` |
| Runtime config | `swust-code.json` or `swust-code.jsonc` |

## Fit

SWUST Code is better suited for repository work that needs more than one turn, such as:

- fixing a set of type, test, or build failures
- completing a refactor, upgrade, or feature in phases
- delegating investigation, implementation, review, or verification to subagents
- keeping project rules and progress across sessions

It is not mainly a short-answer chat interface. For a brief explanation, a normal chat tool is often simpler.

## Relationship To MiMo-Code

The maintenance rule is:

1. If MiMo-Code already provides a capability, keep the MiMo implementation first.
2. If MiMo-Code does not provide it, add the SWUST layer.
3. Keep provider and model names unchanged, including `MiMo Auto`, `mimo/mimo-auto`, and `xiaomi/mimo-*`.

This rule prevents the current mainline from drifting back toward the older OpenCode-era implementation and keeps inherited behavior separate from SWUST-specific additions.
