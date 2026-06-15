---
layout: home

hero:
  name: SWUST Code
  text: Terminal-Native AI Coding Agent
  tagline: Built on OpenCode v1.17.4, prioritizing MiMo Code-style agents, compose, checkpointing, and task runtime while absorbing tooling and cache ideas from DevEco Code and DeepSeek-Reasonix.
  actions:
    - theme: brand
      text: Quick Start
      link: /en/guide/start
    - theme: alt
      text: GitHub
      link: https://github.com/MakeBlackSheepGreat/swust-code

features:
  - icon: 🧠
    title: Persistent Memory
    details: SQLite FTS5 indexing, MEMORY.md injection, @path imports, checkpoint writer, and one-fact-per-file project knowledge.
    link: /en/features/memory
  - icon: 🧭
    title: Agent Modes
    details: main, compose, goal, subagent, and checkpoint-writer now share a MiMo-style runtime model.
    link: /en/features/agents
  - icon: 🎯
    title: Goal-Driven Autonomy
    details: Goal is now a dedicated agent mode with the LLM Judge and continuation reminders.
    link: /en/features/goal
  - icon: 🌱
    title: Self-Improvement
    details: Dream and Distill launch goal-driven autonomous runs and support 7/30-day background triggers.
    link: /en/features/dream
  - icon: 🛡️
    title: Security
    details: 4-step permission pipeline with bash command safety analysis. Fail-closed defaults.
    link: /en/features/security
  - icon: ⚙️
    title: Workflow Engine
    details: JavaScript workflows execute host functions, spawn subagents, and write persistent JSONL journals.
    link: /en/features/workflow
  - icon: 🧩
    title: Skills System
    details: SKILL.md declarative skills, compose hidden skills, and dynamic catalogs are wired into runtime.
    link: /en/features/skills
  - icon: 🌐
    title: Chinese/English TUI
    details: Command palette, permission prompts, language switcher, logo selection, and ghost suggestions are wired.
    link: /en/features/i18n
  - icon: ✦
    title: TUI Experience
    details: Starry home screen, dual logos, SWUST Code theme, and next-prompt suggestions improve terminal use.
    link: /en/features/tui
---
