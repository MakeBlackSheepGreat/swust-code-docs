# SWUST Advantages

This page is not a migration log and not a historical OpenCode audit. It answers a simpler question: **once MiMo-Code is accepted as the runtime base, what does SWUST Code add on top, and what kinds of engineering problems does it handle better than a generic AI coding agent?**

## Why MiMo-Code Is The Base

SWUST Code uses MiMo-Code as its current base because MiMo already connects the runtime pieces that long-running software work needs:

- persistent memory and checkpoints are part of session continuity, not bolt-on features
- actor / subagent orchestration, `goal`, `compose`, Dream / Distill, MCP, LSP, and plugins live in one runtime model
- the terminal TUI, server runtime, and web / desktop surfaces share the same underlying capabilities
- context reconstruction, task tracking, and subagent execution are already on the critical path for long tasks

That makes MiMo a stronger place to continue product work. SWUST does not need to rebuild an older runtime shape first. It can focus on product-layer improvements instead.

## The SWUST Layer Relative To MiMo

MiMo solves the problem of having a capable long-task runtime. The SWUST layer focuses on whether that runtime is easier to use, better governed, and better suited for Chinese-speaking developers in real engineering work.

### Chinese-First TUI And Information Flow

SWUST goes beyond brand replacement by reorganizing the terminal experience around daily usage:

- key commands, prompts, and panels are written with Chinese readability first
- the sidebar emphasizes working directory, Goal, Task, Todo, LSP, MCP, changed files, token, cost, and cache context
- the home page and top-level docs are structured around where to start and what to read next

The benefit is not cosmetic differentiation. The benefit is lower friction during extended terminal work.

### Stronger Engineering Safeguards

MiMo already has a permissions model. SWUST adds more attention to the places where real engineering mistakes happen:

- Task Gate reduces premature stopping when unfinished work still exists
- Bash Safety adds risk analysis for shell execution
- Write Guard narrows writable path boundaries
- Document Validation adds constraints for structured-document work
- cache-stable context layout helps reduce drift in long-running sessions

These additions are meant to reduce operational mistakes, premature completion, and context distortion in real repositories.

### Project-Level Subagent Personalization

MiMo already provides the subagent runtime. SWUST adds a clearer layer for project-level role control:

- `/subagent` and `/subagents` open visible-subagent settings
- different subagents can use different models
- each subagent can have its own reasoning variant
- each subagent can have its own max-step limit

That makes subagents more than generic delegated workers. They become project-governed roles such as lightweight investigators, heavier review agents, short-step executors, or constrained verifiers.

### A Stronger Long-Task Engineering Loop

SWUST emphasizes memory, checkpoints, and Dream / Distill as parts of one long-term project loop:

- memory stores durable rules and project facts
- checkpoints support session recovery and context reconstruction
- Dream consolidates recent work into durable knowledge
- Distill turns repeated actions into skills, commands, subagents, or workflows

The result is that project knowledge can accumulate instead of being re-explained every session.

## What Makes SWUST Different From A Generic Coding Agent

Compared with a generic AI coding agent, SWUST is more directly focused on three problems.

### 1. How Long Tasks Stay Continuous

Many coding agents work well for short tasks, but degrade once work spans multiple stages, files, or sessions:

- constraints get forgotten
- the repository has to be relearned
- unfinished state is not tracked reliably
- quality drops as context grows

SWUST puts memory, checkpoints, Goal, Task, subagents, and context reconstruction on the same path so the task can keep moving.

### 2. How Multi-Agent Work Actually Serves Engineering

Many products treat multi-agent features as a set of named personas. SWUST is more concerned with whether those agents can carry real engineering roles:

- the primary agent drives the main thread of work
- compose handles planning, parallelization, review, and merge structure
- goal handles stop-condition-based autonomous continuation
- subagents handle research, implementation, verification, and checkpoint-related tasks

With project-level subagent configuration, multi-agent behavior becomes a governable role system rather than a display feature.

### 3. How Engineering Risk Is Contained

In real repositories, risk often comes less from a single wrong answer and more from:

- a shell command that should not have run
- a task that should not have stopped
- a path that should not have been written
- a structured document that was modified incorrectly

One of SWUST's distinguishing choices is to treat those risks as first-class runtime concerns.

## Typical Use Cases

| Scenario | Why SWUST fits |
|----------|----------------|
| long-running defect fixing | goal, task state, checkpoints, and memory keep work continuous |
| repository migration and refactoring | work can be split across files, stages, and roles |
| standards-driven development | docs, architecture rules, and long-term constraints can be retained |
| model-assisted review | different subagents can be limited to different models and step budgets |
| repeated engineering flow packaging | dream / distill can turn experience into reusable assets |

## Good Fit And Poor Fit

### Better fit

- continuous development tasks inside real repositories
- long tasks that need resume behavior
- multi-agent work that needs explicit delegation, review, and result recovery
- projects that benefit from durable knowledge accumulation

### Less of a fit

- shallow one-shot prompting
- treating the terminal primarily as a simplified chat window
- temporary scripting questions that do not need memory, task state, or recovery

## In One Line

If MiMo-Code is the base that already solves the long-task runtime problem, then SWUST Code is the product layer that makes that base more suitable for real software engineering through Chinese-first UX, stronger safeguards, subagent governance, and longer-horizon project workflow.
