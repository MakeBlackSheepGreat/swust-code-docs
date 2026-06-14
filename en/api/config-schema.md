# Config Schema

The runtime primarily reads v1 config fields and adapts them into the core v2 config layer. Prefer `swust-code.jsonc` or `.swust-code/swust-code.jsonc` for user configuration.

## Common Fields

| Field | Type | Description |
|-------|------|-------------|
| `$schema` | string | Editor completion URL, currently written as `https://opencode.ai/config.json` |
| `model` | string | Default model in `provider/model` format |
| `small_model` | string | Smaller model for title generation and light tasks |
| `default_agent` | string | Default primary agent |
| `username` | string | Displayed username |
| `permission` | string or object | Tool permission rules |
| `agent` | object | Agent configuration |
| `provider` | object | Custom providers and model overrides |
| `mcp` | object | MCP server configuration |
| `command` | object | Custom slash commands |
| `skills` | object | CLI/TUI v1 skill sources, shaped as `{ paths, urls }` |
| `instructions` | string[] | Additional instruction files or globs |
| `plugin` | array | External plugins |
| `formatter` | boolean or object | Formatter configuration |
| `lsp` | boolean or object | LSP configuration |
| `tool_output` | object | Tool output truncation thresholds |
| `compaction` | object | Context compaction behavior |
| `experimental.predict_next_prompt` | boolean | TUI next-prompt prediction toggle, enabled by default |
| `share` | `manual`, `auto`, `disabled` | Session sharing policy |

## Permissions

```json
{
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow",
    "external_directory": {
      "*": "ask"
    },
    "doom_loop": "ask"
  }
}
```

Permission values are `allow`, `ask`, and `deny`. A field can be a direct string or an object keyed by resource pattern.

## Agents

```json
{
  "default_agent": "build",
  "agent": {
    "build": {
      "model": "anthropic/claude-sonnet-4-6",
      "permission": {
        "bash": "ask",
        "edit": "allow"
      }
    },
    "explore": {
      "mode": "subagent",
      "model": "openai/gpt-4o-mini"
    }
  }
}
```

Built-in agents include `build`, `plan`, `general`, `explore`, `compaction`, `title`, `summary`, `dream`, and `distill`.

## Skills

The current CLI/TUI path reads the v1 shape:

```json
{
  "skills": {
    "paths": [".swust-code/skills", "/absolute/path/to/skills"],
    "urls": ["https://example.com/.well-known/skills/"]
  }
}
```

The core v2 config layer represents `skills` as a string array. The migration layer expands v1 `paths` and `urls` into that array. For user-facing config files, prefer the v1 object shape above.

## Experimental

```json
{
  "experimental": {
    "predict_next_prompt": false,
    "batch_tool": true,
    "openTelemetry": true
  }
}
```

`predict_next_prompt=false` disables TUI next-prompt ghost suggestions. Other experimental fields are wired according to runtime support.
