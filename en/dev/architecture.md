# Architecture

## Runtime Layers

SWUST Code keeps the MiMo-Code runtime foundation and adds a SWUST product layer on top of it. A practical way to read the system is as five layers:

```text
Interface Layer
  CLI / TUI / Web / Desktop / API server

Extension Layer
  Plugins / Skills / MCP / custom commands / integration surfaces

Coordination Layer
  Agent orchestration / subagents / workflow / goal / compose

Execution Layer
  Session runtime / tool registry / permissions / model routing / context rebuild

Foundation Layer
  Effect services / SQLite + Drizzle / config / filesystem / project state
```

## What Matters Most

For everyday users, the most important architectural point is that memory, checkpoints, task state, and subagent execution are not isolated features. They participate in the same runtime path that drives long-running work.

That is why SWUST Code behaves differently from a simple terminal wrapper around an LLM:

- sessions can resume with reconstructed context
- subagents can operate as part of the same engineering workflow
- goal-driven continuation can keep working until a stop condition is actually satisfied
- project knowledge can be retained and gradually refined

## MiMo Base, SWUST Layer

The mainline follows a strict inheritance rule:

- when MiMo-Code already provides the capability, keep the MiMo implementation first
- when MiMo-Code does not provide it, add a SWUST layer with limited surface change

That keeps the runtime cohesive while allowing SWUST to improve Chinese-first UX, engineering safeguards, and project-level control.

## Key SWUST Additions

Within that structure, the most visible SWUST-specific additions are:

- Chinese-first TUI information organization
- richer sidebar context for long terminal sessions
- Task Gate, Bash Safety, Write Guard, and Document Validation
- project-level visible-subagent settings for model, variant, and max steps
- memory organization refinements such as `@path` imports and fact storage

## Why The Architecture Is Shaped This Way

The architecture is optimized for repository-scale work that unfolds over time. That means it prioritizes:

- continuity over one-shot prompting
- explicit task state over implicit intent
- governed delegation over ad hoc agent spawning
- operational safety over unrestricted execution

For API and CLI details, use the main reference pages rather than treating this page as a command catalog.
