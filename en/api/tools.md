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

## TUI/Legacy Tools

| Tool | Description |
|------|-------------|
| `shell` / `bash` | Shell execution, depending on ShellID |
| `read`, `write`, `edit`, `apply_patch` | File read/write and patching |
| `glob`, `grep` | File and content search |
| `task` | Spawn a subagent, optionally in background mode |
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
