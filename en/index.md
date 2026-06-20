---
layout: home

hero:
  name: SWUST Code
  text: "Terminal-native AI coding agent built on MiMo-Code"
  tagline: "Designed for long-running software work. SWUST Code keeps MiMo-Code's runtime strengths for memory, checkpoints, subagent orchestration, goal, Compose, Dream/Distill, MCP, LSP, and plugins, then adds Chinese-first terminal UX, engineering safeguards, and project-level control."
  actions:
    - theme: brand
      text: Quick Start
      link: /en/guide/start
    - theme: alt
      text: SWUST Advantages
      link: /en/DIFFERENCES
    - theme: alt
      text: Mainline Status
      link: /en/mainline-status

features:
  - title: Long-Task Continuity
    details: "Persistent memory, checkpoints, task progress, and context reconstruction help the agent continue work instead of relearning the repository."
    link: /en/features/memory
  - title: Multi-Agent Collaboration
    details: "build, plan, compose, goal, and subagents share one runtime model for planning, parallel execution, review, verification, and autonomy."
    link: /en/features/agents
  - title: Engineering Safeguards
    details: "On top of the MiMo base, SWUST adds Task Gate, Bash Safety, Write Guard, Document Validation, and stronger context governance."
    link: /en/features/security
  - title: Chinese-First TUI
    details: "Sidebar organization, control aliases, feedback surfaces, theme choices, and reading flow are tuned for real daily terminal work."
    link: /en/features/tui
  - title: Evolving Project Knowledge
    details: "/dream and /distill turn durable project knowledge and repeated workflows into reusable memory, skills, subagents, or commands."
    link: /en/features/dream
  - title: Per-Subagent Control
    details: "Visible subagents can be configured with project-level model, reasoning variant, and max-step limits."
    link: /en/features/agents
---

## Product Position

SWUST Code is not trying to be a terminal chat assistant with a thin coding wrapper. It is built around **long-horizon continuity, goal-driven autonomy, subagent coordination, and engineering safeguards** in one runtime model.

It fits work such as:

- repository-scale fixes, migrations, refactors, and validation
- multi-step engineering tasks that need planning, execution, review, and follow-through
- sessions that must resume with context intact rather than restart from scratch
- projects that want to accumulate durable rules, architecture knowledge, and reusable workflows

## Start Here

| Page | Why to read it |
|------|----------------|
| [Quick Start](/en/guide/start) | Install, configure a provider, and learn the daily command surface |
| [Mainline Status](/en/mainline-status) | Understand what the current mainline inherits from MiMo-Code and what SWUST adds |
| [SWUST Advantages](/en/DIFFERENCES) | Understand why the current mainline keeps MiMo first and where the SWUST layer adds product value |
| [Persistent Memory](/en/features/memory) | Learn how memory, checkpoints, and context reconstruction work together |
| [Agent Modes](/en/features/agents) | Learn how build, plan, compose, goal, and subagents cooperate |
| [Workflow Engine](/en/features/workflow) | Learn how multi-agent execution is scripted and resumed |

## Best-Fit Workloads

| Scenario | How SWUST approaches it |
|----------|--------------------------|
| Long-running fixes | goal, task state, and checkpoints keep work moving |
| Multi-stage implementation | compose, subagents, and workflow runtime organize the path |
| Project knowledge accumulation | memory, dream, and distill turn repeated work into durable assets |
| Risky engineering actions | permission layers, bash safety, and write guards reduce operational mistakes |

## What It Does Not Optimize For

SWUST Code is not primarily optimized for short one-shot prompting or demo-style coding. Its design target is real repositories, real constraints, and long-running engineering work.
