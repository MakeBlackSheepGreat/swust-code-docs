---
layout: home

hero:
  name: SWUST Code
  text: "Terminal-native AI coding agent built on MiMo-Code"
  tagline: "A coding agent for long-running software work. It keeps MiMo-Code as the runtime base for memory, checkpoints, actor orchestration, goal, Compose, Dream/Distill, voice, MCP, LSP, and plugins, then layers SWUST-specific Chinese UX and engineering safeguards on top."
  actions:
    - theme: brand
      text: Quick Start
      link: /en/guide/start
    - theme: alt
      text: Status
      link: /en/mainline-status
    - theme: alt
      text: GitHub
      link: https://github.com/MakeBlackSheepGreat/swust-code

features:
  - title: MiMo-Code Base First
    details: "Existing MiMo capabilities stay native: providers, TUI, memory, checkpoints, actors/subagents, goal, Compose, Dream/Distill, voice, MCP, LSP, and plugins."
    link: /en/mainline-status
  - title: Long-Task Continuity
    details: "Persistent memory, checkpoints, task progress, and context reconstruction help the agent resume work instead of relearning the project."
    link: /en/features/memory
  - title: Multi-Agent Workflows
    details: "build, plan, compose, and goal agents work with subagent orchestration for exploration, implementation, review, TDD, verification, and specs-driven development."
    link: /en/features/agents
  - title: Goal-Driven Autonomy
    details: "Use /goal or run --goal to set a stop condition. An independent judge checks whether the goal is truly complete before the session stops."
    link: /en/features/goal
  - title: Memory And Skill Distillation
    details: "/dream consolidates durable project knowledge, while /distill turns repeated workflows into reusable skills, subagents, or commands."
    link: /en/features/dream
  - title: Engineering Safeguards
    details: "The SWUST layer adds Task Gate, Bash Safety, Write Guard, Document Validation, cache-stable context, and @path memory imports."
    link: /en/features/security
  - title: Chinese-First TUI
    details: "Sidebar, command palette, permission prompts, getting-started hints, path display, themes, attention notifications, and sound packs are tuned for daily terminal work."
    link: /en/features/tui
---
