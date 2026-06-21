---
layout: home

hero:
  name: SWUST Code
  text: "龙山灵码"
  tagline: "A terminal AI coding tool based on MiMo-Code. It keeps the MiMo-Code long-task runtime and adds a SWUST layer for Chinese TUI work, engineering safeguards, memory organization, and project-level subagent settings."
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
    <p class="swust-kicker">CURRENT LINE</p>
    <dl>
      <div><dt>Declared version</dt><dd>v0.6.0</dd></div>
      <div><dt>Runtime base</dt><dd>MiMo-Code</dd></div>
      <div><dt>CLI</dt><dd><code>swust-code</code></dd></div>
      <div><dt>Project dir</dt><dd><code>.swust-code/</code></dd></div>
    </dl>
  </div>
</section>

## Current Mainline

| Module | Current behavior |
|--------|------------------|
| MiMo-Code base | memory, checkpoints, subagents, `goal`, `compose`, MCP, LSP, and plugins follow the current MiMo mainline. |
| Resumable long tasks | `MEMORY.md`, facts, `checkpoint.md`, and task progress store project facts, session state, and task progress. |
| Subagent settings | Use `/subagent` to set model, variant, and max steps for visible subagents. Settings are stored in project config. |

## Check These First

| Question | Current answer | Read next |
|----------|----------------|-----------|
| What is the current mainline based on? | MiMo-Code. Existing MiMo behavior stays first. | [Mainline Status](/en/mainline-status) |
| What does SWUST add? | Chinese TUI work, Task Gate, Bash Safety, Write Guard, Document Validation, project-level `/subagent` settings, and related guardrails. | [SWUST Advantages](/en/DIFFERENCES) |
| How do I start? | Install the CLI, run `swust-code` in a repository, then configure a provider from the startup guide. | [Quick Start](/en/guide/start) |

## Good Fit

SWUST Code is intended for repository work that continues across multiple steps:

- multi-file fixes, refactors, migrations, and upgrades
- long tasks that need `goal` to check completion
- tasks that benefit from subagent research, implementation, review, or verification
- projects that need rules, facts, and progress to survive across sessions

For a short conceptual answer, a normal chat tool is usually simpler.

## MiMo Base And SWUST Layer

| Layer | Contents | How to describe it |
|-------|----------|--------------------|
| MiMo-Code base | memory, checkpoints, actor / subagent runtime, `goal`, `compose`, Dream / Distill, MCP, LSP, plugins, TUI / Server Runtime | Treat these as inherited MiMo capabilities. |
| SWUST layer | Chinese-first information flow, sidebar work, engineering safeguards, memory path guards, document validation, project-level subagent settings | Describe these as SWUST additions only where the behavior is actually added or changed by SWUST. |

## Common Entry Points

| Goal | Page |
|------|------|
| Install, first launch, provider setup | [Quick Start](/en/guide/start) |
| Understand the main agent, `goal`, `compose`, and subagents | [Agent Modes](/en/features/agents) |
| Understand `MEMORY.md`, facts, and checkpoints | [Persistent Memory](/en/features/memory) |
| Read about Task Gate, Bash Safety, and Write Guard | [Security](/en/features/security) |
| Check CLI commands and config fields | [CLI Commands](/en/api/commands), [Config Schema](/en/api/config-schema) |

## Naming Boundary

Provider and model names are not rebranded:

- `MiMo Auto`
- Xiaomi MiMo Platform
- `mimo/mimo-auto`
- `xiaomi/mimo-*`

These are provider or model identifiers, not SWUST product copy.
