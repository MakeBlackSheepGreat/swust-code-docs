# SWUST Advantages

SWUST Code is built on the MiMo-Code long-task runtime and adds a SWUST layer for Chinese terminal use, engineering safeguards, project-memory organization, and subagent configuration.

MiMo-Code provides memory, checkpoints, subagents, `goal`, `compose`, Dream / Distill, MCP, LSP, and plugins. The SWUST layer adds behavior around daily terminal use and repository-level risk.

## Chinese-First Terminal Experience

The usefulness of a terminal tool depends heavily on whether state and actions are easy to scan. SWUST Code focuses first on the text and panels that Chinese-speaking users see every day:

- command descriptions, prompts, and common dialogs use Chinese wording
- the sidebar shows working directory, Goal, Task, Todo, LSP, MCP, changed files, token usage, cost, and cache state
- getting-started prompts point to common entry points
- the theme uses deep blue as the main color instead of keeping MiMo's orange home-screen identity

These interface changes reduce the time spent looking for state and commands in the terminal.

## Long-Task Context

Real repository tasks often span many turns. If the system only relies on chat history, context grows too long, early constraints fade, and resumed sessions need the project explained again.

The current mainline uses MiMo-Code memory and checkpoint behavior and adds SWUST memory-organization details:

- `MEMORY.md` stores durable project rules
- the facts directory stores project facts one file at a time
- `@path` imports split larger memory files into smaller topics
- `/memory` searches durable project knowledge
- checkpoints record recovery state when a session approaches context pressure

These mechanisms let a later session resume from project state.

## Engineering Safeguards

An AI coding tool can execute shell commands, write files, and edit documents inside a repository. A bad command, bad write target, or premature stop can affect later steps.

The SWUST layer adds several safeguards:

- Task Gate checks unfinished work and reduces premature stopping
- Bash Safety analyzes risky shell commands such as destructive deletion, download-and-execute, and force reset
- Write Guard narrows memory and project-file write boundaries
- Document Validation checks structure when editing structured documents
- cache-stable prefix reduces cache and noise issues caused by changing context prefixes during long tasks

These safeguards do not replace human judgment, but they reduce common automation failures in long-running work.

## Subagent Configuration

MiMo-Code already provides the subagent runtime. SWUST Code adds project-level configuration:

```text
/subagent
/subagents
```

Visible subagents can be configured with:

- model
- reasoning variant
- max execution steps
- cleared project overrides

This lets different roles use different policies. For example, an investigation subagent can use a faster model, a review subagent can use stronger reasoning, and a verifier can have a tighter step limit.

## Good Fits

Good fits include:

- fixing a connected set of failures
- completing refactors or migrations in stages
- using subagents for research, implementation, review, and verification
- preserving project rules, debugging conclusions, and repeated workflows

For a short explanation, a normal chat tool is usually faster.
