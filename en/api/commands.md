# CLI Commands

## Global Options

| Option | Description |
|--------|-------------|
| `--help`, `-h` | Show help |
| `--version`, `-v` | Show version |
| `--print-logs` | Print logs to stderr |
| `--log-level DEBUG\|INFO\|WARN\|ERROR` | Set log level |
| `--pure` | Disable external plugins |

## Core Commands

| Command | Description |
|---------|-------------|
| `swust-code` | Start the interactive TUI |
| `swust-code run [message]` | Run one prompt |
| `swust-code run --goal "goal" "message"` | Goal-driven run mode |
| `swust-code dream` | Start the memory consolidation command flow |
| `swust-code distill` | Start the workflow packaging command flow |
| `swust-code serve` | Start a headless API server |
| `swust-code web` | Start the server and open the Web UI |
| `swust-code attach <url>` | Attach to an existing server |

## `run` Options

```bash
swust-code run [message..]

Options:
  -c, --continue          Continue the last session
  -s, --session           Continue a specific session ID
  -m, --model             Model in provider/model format
  --goal                  Set an autonomous goal
  --agent                 Select an agent
  --fork                  Fork before continuing
  --share                 Share the session
  --format default|json   Output format
  -f, --file              Attach file(s)
  --title                 Session title
  --attach                Attach to a remote server
  --dir                   Working directory
  --interactive, -i       Direct interactive mode
  --thinking              Show thinking blocks
  --variant               Provider-specific model variant
```

## Management Commands

| Command | Description |
|---------|-------------|
| `swust-code providers list` | List provider credentials |
| `swust-code providers login [url]` | Log in to a provider |
| `swust-code providers logout [provider]` | Remove provider credentials |
| `swust-code providers import` | Import credentials from MiMo-Code, Claude Code, or env vars |
| `swust-code agent` | Manage agents |
| `swust-code mcp list` | List MCP servers |
| `swust-code mcp add` | Add an MCP server |
| `swust-code mcp auth [name]` | Run OAuth for a remote MCP server |
| `swust-code models [provider]` | List models |
| `swust-code plugin <module>` | Install a plugin |
| `swust-code session` | Manage sessions |
| `swust-code db` | Database tools |
| `swust-code stats` | Token and cost stats |
| `swust-code export [sessionID]` | Export session JSON |
| `swust-code import <file>` | Import session JSON or share URL |
| `swust-code github` | Manage GitHub agent |
| `swust-code pr <number>` | Checkout a PR and run SWUST Code |
| `swust-code acp` | Start Agent Client Protocol server |
| `swust-code upgrade` | Upgrade |
| `swust-code uninstall` | Uninstall |
