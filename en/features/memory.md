# Persistent Memory

SWUST Code's memory system lets your AI coding assistant remember project knowledge across sessions.

## How It Works

Memory is stored as Markdown files and reconciled into a SQLite FTS5 full-text index. The core v2 runner loads memory context during system prompt assembly and injects global `MEMORY.md` content with a 4KB cap. When long sessions approach the context limit, v0.4 can start the checkpoint writer before rebuilding context from a checkpoint boundary.

## Memory Directory Structure

```
~/.local/share/swust-code/memory/
  global/
    MEMORY.md              # Cross-project preferences
  projects/
    <project_hash>/
      MEMORY.md            # Project knowledge
      facts/
        <fact>.md          # One-fact-per-file store
  sessions/
    <session_id>/
      checkpoint.md        # Session checkpoint (11 sections)
      notes.md             # Temporary notes
      tasks/
        <task_id>/
          progress.md      # Subagent task progress
```

## Memory Tools

- `memory` — Search persistent knowledge in the core v2 registry
- `memory_write` — Write structured knowledge to memory files in the core v2 registry

## Automatic Behavior

- **Pre-search sync**: Automatically syncs disk files to FTS index before each search
- **Context injection**: Auto-injects MEMORY.md content into system prompt (4KB cap)
- **Incremental sync**: Fingerprints based on file size and mtime, only processes changed files
- **Imports**: `MEMORY.md` supports `@path` imports during local resolution
- **Checkpoint writer**: A background system agent writes `checkpoint.md`, `MEMORY.md`, and task progress summaries
- **Boundary rebuild**: `last_checkpoint_message_id` records the checkpoint boundary for future context rebuilds
