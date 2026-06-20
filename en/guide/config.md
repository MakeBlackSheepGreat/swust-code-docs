# Configuration

SWUST Code uses JSON/JSONC config files for models, permissions, providers, MCP, agents, plugins, and TUI behavior.

## Config Locations

| Scope | Paths |
|-------|-------|
| Global | `~/.config/swust-code/swust-code.json`, `~/.config/swust-code/swust-code.jsonc` |
| Project | `swust-code.json`, `swust-code.jsonc` discovered upward from the current directory |
| Project directory | `.swust-code/swust-code.json`, `.swust-code/swust-code.jsonc` |
| TUI | `~/.config/swust-code/tui.json`, project-root `tui.json`, and `tui.jsonc` variants |

Project config overrides global config, and the closest project config wins. Use `SWUST_CODE_CONFIG` for one explicit file or `SWUST_CODE_CONFIG_DIR` for an additional config directory.

## Basic Config

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-4-6",
  "permission": {
    "bash": "ask",
    "edit": "allow",
    "read": "allow"
  }
}
```

## Skill Sources

```json
{
  "skills": {
    "paths": [".swust-code/skills"],
    "urls": ["https://example.com/.well-known/skills/"]
  }
}
```

The CLI/TUI path currently reads this v1 object shape. The core v2 layer adapts these entries into local directory or remote URL sources internally.

## Experimental Options

```json
{
  "experimental": {
    "predict_next_prompt": true
  }
}
```

`predict_next_prompt` controls the TUI next-prompt ghost suggestion. It is enabled by default. Set it to `false` to hide ghost suggestions in empty prompt input.

## Environment Variables

| Variable | Description |
|----------|-------------|
| `SWUST_CODE_CONFIG` | Use one explicit config file |
| `SWUST_CODE_CONFIG_DIR` | Custom config directory |
| `SWUST_CODE_CONFIG_CONTENT` | Inject config content from an environment variable |
| `SWUST_CODE_DISABLE_PROJECT_CONFIG` | Disable project config discovery |
| `SWUST_CODE_DB` | Custom database path |
| `SWUST_CODE_PURE` | Disable external plugins |
| `SWUST_CODE_DISABLE_MODELS_FETCH` | Disable model catalog refresh |
| `SWUST_CODE_SERVER_PASSWORD` | Password for `serve` and `web` |
| `SWUST_CODE_SERVER_USERNAME` | Username for `serve` and `web` |
| `SWUST_CODE_LOCALE` | Pin TUI language preference, such as `auto`, `en`, or `zh` |
| `SWUST_CODE_AUTO_EVOLUTION` | Set to `0` or `false` to disable background Dream/Distill auto-triggers |
| `SWUST_CODE_MEMORY_RECONCILE_ON_SEARCH` | Auto-sync memory before search (default: true) |
