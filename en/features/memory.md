# Persistent Memory

SWUST Code's memory system stores project rules, historical facts, and session recovery information. It works with checkpoints and context reconstruction to support long-running work.

## Why Memory Matters For Long Tasks

In real repositories, long-running tasks need the system to:

- remember project constraints in the next phase
- resume later without losing where the work stopped
- bring subagent findings back into the main task
- survive context pressure without collapsing continuity

That is why SWUST places memory, checkpoints, and context reconstruction on the same runtime path.

## Three Memory Scopes

| Scope | Best used for |
|-------|---------------|
| `global` | personal preferences and cross-project habits |
| `projects/<project-id>` | architecture constraints, project rules, durable facts |
| `sessions/<session-id>` | temporary notes, checkpoints, task progress |

This separation keeps user-level, project-level, and session-level information from being mixed into one undifferentiated file.

## How Memory Works With Checkpoints

Long-task continuity usually follows this sequence:

1. the session loads project memory and relevant global memory
2. the agent searches existing knowledge with `/memory` and writes new facts when needed
3. when context pressure grows, checkpointing writes `checkpoint.md`, `notes.md`, and task progress
4. on resume, memory, checkpoints, and the recent tail are rebuilt into a usable working context

Memory answers "what should still be known later." Checkpoints answer "where did this session get to."

## Directory Structure

```text
~/.local/share/swust-code/memory/
  global/
    MEMORY.md
  projects/
    <project-id>/
      MEMORY.md
      facts/
        <fact>.md
  sessions/
    <session-id>/
      checkpoint.md
      notes.md
      tasks/
        <task-id>/
          progress.md
```

Two design choices matter here:

- project facts can be stored one fact per file
- `MEMORY.md` supports `@path` imports for better topical organization

That makes the knowledge base easier to maintain over time.

## Search And Consolidation

SWUST Code reconciles memory files into a SQLite FTS5 index for full-text retrieval. In daily use, the important actions are:

- `/memory <query>` for retrieval
- `/dream` and `/distill` for consolidation and packaging

More specifically:

- `/dream` is oriented toward retaining durable project knowledge
- `/distill` is oriented toward turning repeated work into reusable assets

Both exist to reduce re-explanation in future work.

## What Belongs In Memory

The following are usually good project-memory candidates:

- durable architecture decisions
- recurring pitfalls and boundary conditions
- repository conventions and naming rules
- debugging conclusions that keep reappearing

The following are usually better kept at the session layer:

- one-off experiments
- unconfirmed guesses
- local observations that will quickly expire

Memory files should prioritize content that remains useful over time, not every temporary observation.
