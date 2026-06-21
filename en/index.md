---
layout: home

hero:
  name: SWUST Code
  text: "Terminal-native AI coding agent built on MiMo-Code"
  tagline: "Work inside real repositories from the terminal: read code, edit files, run commands, delegate to subagents, write checkpoints, and keep project knowledge for the next session."
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
    details: "Memory, checkpoints, task progress, and context reconstruction work together so resumed sessions do not start from zero."
    link: /en/features/memory
  - title: Multi-Agent Collaboration
    details: "build, plan, compose, goal, and subagents share one runtime path for planning, execution, review, and verification."
    link: /en/features/agents
  - title: Engineering Safeguards
    details: "Task Gate, Bash Safety, Write Guard, and Document Validation handle premature stops, risky shell commands, bad writes, and structured-document errors."
    link: /en/features/security
  - title: Chinese-First TUI
    details: "Sidebar layout, command aliases, prompts, feedback, and theme choices are tuned for daily terminal work by Chinese-speaking developers."
    link: /en/features/tui
  - title: Evolving Project Knowledge
    details: "/dream consolidates durable knowledge; /distill packages repeated work into skills, commands, subagents, or workflows."
    link: /en/features/dream
  - title: Per-Subagent Control
    details: "/subagent sets project-level model, reasoning variant, and max-step limits for visible subagents."
    link: /en/features/agents
---

<div class="swust-signal-row">
  <a class="swust-signal" href="/en/mainline-status">
    <span class="swust-signal-label">Mainline</span>
    <strong>MiMo-Code base</strong>
    <span>v0.6.0</span>
  </a>
  <a class="swust-signal" href="/en/features/agents">
    <span class="swust-signal-label">Agents</span>
    <strong>build / plan / compose / goal</strong>
    <span>project-level subagent settings</span>
  </a>
  <a class="swust-signal" href="/en/features/memory">
    <span class="swust-signal-label">Continuity</span>
    <strong>memory + checkpoint</strong>
    <span>resume, compact, rebuild context</span>
  </a>
</div>

<div class="swust-terminal">
  <div class="swust-terminal-bar">
    <span></span><span></span><span></span>
    <strong>swust-code</strong>
  </div>
  <div class="swust-terminal-body">

```bash
$ swust-code
> /goal fix type errors and update tests
> /subagent
> /dream
```

  </div>
</div>

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

## Four Tracks

<div class="swust-flow-grid">
  <a class="swust-flow-card" href="/en/features/agents">
    <span>01</span>
    <strong>Agent Roles</strong>
    <p>Use build, plan, compose, goal, and subagents for the main thread, research, orchestration, autonomy, and local execution.</p>
  </a>
  <a class="swust-flow-card" href="/en/features/memory">
    <span>02</span>
    <strong>Memory And Resume</strong>
    <p>Use MEMORY.md, facts, checkpoints, and task progress to preserve context that can continue later.</p>
  </a>
  <a class="swust-flow-card" href="/en/features/security">
    <span>03</span>
    <strong>Engineering Safeguards</strong>
    <p>Handle risky shell commands, bad writes, premature stops, and structured-document mistakes in the runtime.</p>
  </a>
  <a class="swust-flow-card" href="/en/features/workflow">
    <span>04</span>
    <strong>Workflow Packaging</strong>
    <p>Turn repeated multi-agent processes into recoverable, recorded, repeatable workflows.</p>
  </a>
</div>

## Best-Fit Workloads

| Scenario | How SWUST approaches it |
|----------|--------------------------|
| Long-running fixes | goal, task state, and checkpoints keep work moving |
| Multi-stage implementation | compose, subagents, and workflow runtime organize the path |
| Project knowledge accumulation | memory, dream, and distill turn repeated work into durable assets |
| Risky engineering actions | permission layers, bash safety, and write guards reduce operational mistakes |

## What It Does Not Optimize For

SWUST Code is not primarily optimized for short one-shot prompting or demo-style coding. Its design target is real repositories, real constraints, and long-running engineering work.
