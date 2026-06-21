# SWUST Advantages

This page explains how SWUST Code relates to MiMo-Code and what behavior the SWUST layer adds. It is not a migration log, and it does not rename MiMo features as SWUST inventions.

## The Problem

AI coding work inside a real repository is rarely finished in one answer. Common failure modes include:

- early constraints disappear when the context grows
- a resumed session needs the project state explained again
- subtasks can be delegated, but roles lack project-level limits
- shell execution, file writes, and structured-document edits create engineering risk
- Chinese terminal users need direct command text, state, and sidebar information

MiMo-Code already solves much of the runtime foundation. SWUST Code keeps that base and adds a SWUST layer on top.

## What MiMo-Code Provides

The current mainline inherits the MiMo-Code long-task runtime:

| Capability | Purpose |
|------------|---------|
| memory / checkpoint | store project facts, session state, and recovery context |
| actor / subagent | delegate work to independent roles and return results to the main session |
| `goal` | check whether the stopping condition has actually been met |
| `compose` | organize planning, parallel execution, review, and result integration |
| Dream / Distill | turn recent work into durable knowledge or reusable flows |
| MCP / LSP / plugin / skill | connect tools, language services, and project extensions |

These capabilities should be described as MiMo base capabilities. SWUST does not rewrite these mechanisms or move the mainline back toward the older OpenCode-era shape.

## What The SWUST Layer Adds

### Chinese-First Terminal Information

The SWUST layer changes high-frequency terminal information for Chinese-speaking users:

- command descriptions and common entry points use Chinese wording
- the sidebar emphasizes working directory, Goal, Task, Todo, LSP, MCP, changed files, token usage, cost, and cache state
- the home page, quick start, and feature pages are organized around the user's next action instead of implementation history

The standard is not whether the UI looks different. The standard is whether the user can find task-relevant state faster.

### Engineering Safeguards

The SWUST layer gives several high-risk areas their own handling:

| Module | Problem handled |
|--------|-----------------|
| Task Gate | reduces premature stopping while unfinished tasks remain |
| Bash Safety | adds risk analysis for shell commands |
| Write Guard | narrows memory and project write boundaries |
| Document Validation | checks structure when editing structured documents |
| cache-stable prefix | reduces noise from context-prefix drift during long tasks |

These modules do not replace MiMo's permission system. They add more specific engineering boundaries.

### Project-Level Subagent Settings

MiMo already provides the subagent runtime. SWUST adds a project-level settings entry:

```text
/subagent
/subagents
```

Visible subagents can be configured with:

- model
- reasoning variant
- max execution steps
- cleared overrides to return to default behavior

Settings are written into project-level `agent` config instead of global defaults. This lets one project give investigation, implementation, review, and verification roles different model and step policies.

### Memory Organization Additions

SWUST keeps MiMo memory and checkpoint behavior and adds a clearer project-knowledge organization layer:

- `MEMORY.md` supports `@path` imports
- project facts can be stored as one-fact-per-file
- write targets are checked by guards
- `/memory` searches durable project knowledge

The goal is to reduce repeated project explanation while keeping memory files maintainable.

## Compared With A Generic Coding Agent

A generic coding agent often optimizes for single-turn generation. SWUST Code focuses more on what happens when work continues over time.

| Problem | Common approach | SWUST Code approach |
|---------|-----------------|---------------------|
| Long session | summarize or drop history | recover necessary state through memory, checkpoints, and context reconstruction |
| Many subtasks | manually split prompts | use subagent / compose / goal for research, execution, review, and completion checks |
| Many project rules | repeat reminders | store rules in project memory and fact files, then re-inject on recovery |
| Risky operations | rely on manual review | use permissions plus Task Gate, Bash Safety, Write Guard, and Document Validation |

## When It Fits

Better fit:

- repository tasks that need multiple turns
- refactors, migrations, upgrades, and batch fixes
- work that benefits from subagent role separation
- projects that need rules and progress to persist across sessions

Not the best fit:

- one-shot conceptual explanations
- short questions without repository context
- temporary questions that do not need memory, checkpoints, or tool calls

## Maintenance Rule

Future work follows this order:

1. If MiMo-Code already provides a feature, keep the current MiMo implementation first.
2. If MiMo-Code does not provide it and SWUST needs it, add it as a SWUST layer.
3. Keep provider and model names unchanged, including `MiMo Auto`, `mimo/mimo-auto`, and `xiaomi/mimo-*`.
4. Public docs describe stable capabilities, not temporary branches, PR states, or agent-session process.
