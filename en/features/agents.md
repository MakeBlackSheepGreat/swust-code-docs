# Agent Modes

SWUST Code places the primary agent, `goal`, `compose`, subagents, and system agents inside one runtime model. The practical benefit is that planning, execution, review, resume, and consolidation do not have to depend on disconnected subsystems.

## One Runtime, Different Roles

In everyday use, it helps to think of SWUST Code as a coordinated role system:

- the primary agent drives the main thread of work
- `plan` handles read-only exploration and solution shaping
- `compose` handles planning, parallelization, review, and merge structure
- `goal` handles continued work against a stop condition
- subagents handle delegated task units
- system agents handle checkpoints, memory consolidation, and workflow packaging

Because these roles share one runtime path, they can reuse task state, context recovery, and execution boundaries more cleanly.

## Primary Agent Roles

| Agent | Best used for |
|-------|---------------|
| `build` | default implementation, fixing, direct tool use |
| `plan` | read-only investigation, design, risk assessment |
| `compose` | large-task decomposition, parallel work, review, verification, merge |
| `goal` | autonomous continuation with an explicit stop condition |

If you already know the next step, `build` or `plan` is often enough. `compose` and `goal` become more valuable once the work needs explicit orchestration.

## How Subagents Participate

Subagents are not a separate product surface. They are role extensions inside the current work chain:

- they can advance an isolated subtask
- they can run in the foreground or continue in the background
- their results and state flow back into the main task path
- they can participate in the same checkpoint, task, and memory lifecycle

The runtime also uses dedicated system agents such as:

- `checkpoint-writer`
- `dream`
- `distill`

You usually do not manage those directly, but they explain why SWUST Code can keep moving in long-running work instead of behaving like a single-turn assistant.

## Project-Level `/subagent` Configuration

The current mainline adds a project-level configuration entry point for visible subagents:

- `/subagent`
- `/subagents`

From that interface, you can set for each visible subagent:

- a dedicated model
- a dedicated reasoning variant
- a max-step limit
- or clear overrides and return to the default behavior

These settings live at the project level rather than becoming global defaults. That makes them useful for repository-specific role control, such as:

- faster, cheaper investigation subagents
- stronger review subagents with heavier reasoning
- tightly bounded verifier subagents with short step budgets

## How `compose`, `goal`, And Subagents Relate

These three capabilities are often lumped together, but they solve different problems:

| Capability | Main job |
|------------|----------|
| `compose` | give a complex task structure and phases |
| `goal` | keep checking whether the task is actually done before stopping |
| subagents | hand local units of work to separate roles |

A common large-task flow looks like this:

1. use `plan` or `compose` to understand and break down the work
2. use subagents for investigation, implementation, or verification
3. use `goal` to prevent premature stopping
4. let checkpoints take over when session pressure grows

## When To Use Which

| Situation | Recommended path |
|-----------|------------------|
| quick implementation or bug fix | `build` |
| read-only repository exploration | `plan` |
| large task with decomposition and review | `compose` |
| explicit objective with continued execution | `goal` |
| isolated role for one local task | subagent |
| long-session recovery or knowledge consolidation | `checkpoint-writer`, `dream`, `distill` |
