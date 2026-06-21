---
layout: home

hero:
  name: SWUST Code
  text: "龙山灵码"
  tagline: "A terminal tool for long-running software engineering tasks. Built on MiMo-Code, it provides memory, checkpoints, subagents, goal-driven execution, and a Chinese-first TUI."
  actions:
    - theme: brand
      text: Quick Start
      link: /en/guide/start
    - theme: alt
      text: GitHub
      link: https://github.com/MakeBlackSheepGreat/swust-code
    - theme: alt
      text: NPM
      link: https://www.npmjs.com/package/@swust-code/cli
---

<section class="swust-home-intro">
  <div class="swust-install">
    <p class="swust-kicker">INSTALL</p>
    <pre><code>npm install -g @swust-code/cli
swust-code</code></pre>
  </div>
  <div class="swust-facts">
    <p class="swust-kicker">FACTS</p>
    <dl>
      <div><dt>Version</dt><dd>v0.6.0</dd></div>
      <div><dt>Base</dt><dd>MiMo-Code</dd></div>
      <div><dt>Command</dt><dd><code>swust-code</code></dd></div>
      <div><dt>Project assets</dt><dd><code>.swust-code/</code></dd></div>
    </dl>
  </div>
</section>

## What It Is For

SWUST Code is most useful inside an existing repository, especially when the work cannot be finished in one turn:

- fixing a set of test, type, or build failures
- completing a refactor, migration, or feature in stages
- delegating research, implementation, review, or verification to subagents
- keeping project rules, findings, and progress across sessions

For a short conceptual explanation, a normal chat tool is usually simpler.

## Core Capabilities

### Keep Project Context

Project memory stores durable rules and facts. When a session approaches the context limit, checkpoints record progress and help rebuild the next working context.

Read: [Persistent Memory](/en/features/memory)

### Split Long Tasks

`goal` describes a completion condition in natural language, `compose` structures complex work, and subagents handle local research, implementation, or verification.

Read: [Agent Modes](/en/features/agents)

### Reduce Engineering Risk

Task Gate, Bash Safety, Write Guard, and Document Validation handle premature stopping, risky shell commands, out-of-bounds writes, and structured-document edits.

Read: [Security](/en/features/security)

### Package Repeated Work

`/dream` consolidates project knowledge. `/distill` turns repeated actions into skills, commands, subagents, or workflows.

Read: [Workflow Engine](/en/features/workflow)

## Start Here

| Goal | Page |
|------|------|
| Install and complete the first launch | [Quick Start](/en/guide/start) |
| Configure models and providers | [LLM Providers](/en/guide/providers) |
| Understand subagents, `goal`, and `compose` | [Agent Modes](/en/features/agents) |
| Check CLI commands and config fields | [CLI Commands](/en/api/commands), [Config Schema](/en/api/config-schema) |
| Read the current version status | [Mainline Status](/en/mainline-status) |
