# Tools

SWUST Code currently has two tool registration paths: the core v2 runner uses `packages/core/src/tool/`, while the TUI/legacy session path uses `packages/opencode/src/tool/`. The tool list visible in a session depends on the active runtime.

## Core v2 Built-ins

| Tool | Description |
|------|-------------|
| `bash` | Execute a shell command with safety analysis |
| `read` | Read files or images |
| `write` | Write files |
| `edit` | Precise file editing |
| `apply_patch` | Apply patches |
| `glob` | File pattern search |
| `grep` | Content search via ripgrep |
| `webfetch` | Fetch web content |
| `websearch` | Search the web |
| `memory` | Search persistent memory with FTS5 + BM25 |
| `memory_write` | Write persistent memory |
| `todowrite` | Manage task state |
| `question` | Ask the user a question |
| `skill` | Load SKILL.md content |
| `history` | Search historical sessions through History FTS |

## TUI/Legacy Tools

| Tool | Description |
|------|-------------|
| `shell` / `bash` | Shell execution, depending on ShellID |
| `read`, `write`, `edit`, `apply_patch` | File read/write and patching |
| `glob`, `grep` | File and content search |
| `task` | Spawn a subagent, optionally in background mode |
| `actor` | MiMo-style Actor API: run, spawn, status, wait, cancel, send |
| `subagent` | Dedicated subagent dispatch tool |
| `workflow` | Invoke scripted workflows |
| `memory` | Search or write memory |
| `history` | Query historical sessions and snippets |
| `webfetch`, `websearch` | Web fetch and search |
| `skill` | Load a skill |
| `lsp` | Experimental LSP tool |
| `plan_exit` | Experimental Plan-mode exit tool |

## Safety Attributes

Core v2 tools declare:

- `isReadOnly`
- `isConcurrencySafe`
- `isDestructive`, defaulting to true

Bash commands are classified as `safe`, `caution`, or `dangerous` before execution.

## Actor Tool

v0.4 exposes the MiMo-style Actor API:

| Operation | Description |
|-----------|-------------|
| `run` | Run a subagent in the foreground and wait for the result |
| `spawn` | Start a background subagent and return an actor id |
| `status` | Read actor status from the registry |
| `wait` | Wait for a background actor |
| `cancel` | Cancel an actor |
| `send` | Send an Inbox message to an actor |

Background actors expose waitable outcomes. Task-bound actors update Task Registry based on return headers and runtime completion checks.
