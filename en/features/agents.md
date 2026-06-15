# Agent Modes

v0.4 moves SWUST Code closer to MiMo Code's runtime model. `compose`, `goal`, the main agent, background subagents, and system agents now share the same agent-mode framing, so prompts, skill catalogs, message slices, task state, and background notifications can use one runtime path.

## Mode Overview

| Mode | Entry | Purpose |
|------|-------|---------|
| `main` | Default session | Normal coding, Q&A, and tool calls |
| `compose` | `--agent compose` or config | Planning, parallel work, review, verification, and merge workflows |
| `goal` | `swust-code run --goal ...` | Goal-driven autonomy with continuation checks |
| subagent | `actor`, `subagent`, workflow | Delegated foreground or background work |
| `checkpoint-writer` | System-triggered | Writes `checkpoint.md`, `MEMORY.md`, and task progress summaries |
| `dream` / `distill` | CLI or scheduled trigger | Memory consolidation and skill discovery |

## Compose Agent

The compose agent carries MiMo-style bundled skills such as `plan`, `parallel`, `review`, `verify`, `merge`, `subagent`, and `tdd`. These skills are hidden from regular agents and are injected only when the message agent is `compose`.

## Goal Agent

`swust-code run --goal "..."` now routes to the `goal` agent when `--agent` is omitted. Explicit `--agent` selection still wins. Goal mode keeps the v0.3 LLM Judge and Goal Gate, while adding a dedicated prompt and reminders.

## Actor Runtime

Actor Spawn now follows the MiMo shape:

- subagents write to the parent session under their own `agentID` slice;
- peer actors still use child sessions for isolation;
- background actors expose a waitable outcome;
- `preStop` and `postStop` hooks can request ReAct re-entry;
- task binding, return-header reconciliation, Inbox, Actor Registry, and Task Registry are durable.

## Checkpoint Writer

The checkpoint writer is now a real background system agent. It uses a child session, receives `parentSessionID` for plugin path resolution, maintains a one-slot pending queue, and advances `last_checkpoint_message_id` after settlement.

