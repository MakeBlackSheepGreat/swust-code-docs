# TUI Experience

v0.3 moves the TUI from basic translation coverage into visible interaction polish: command palette, permission prompts, home screen, logo selection, and prompt input all use the newer localization and visual paths.

## Command Palette

Command names and slash entries remain stable, such as `/models`, `/language`, and `/logo`. Descriptions and categories are localized according to the active language, so shortcuts stay predictable while the explanatory text changes.

## Language Switcher

```text
/language
```

The language preference is stored in TUI KV:

- `auto`: follow system detection
- `en`: English
- `zh`: Simplified Chinese
- Other locale codes currently have labels and types; dictionaries still need to be added

`SWUST_CODE_LOCALE` has higher priority and can pin the startup language.

## Logo And Home Screen

```text
/logo
```

The TUI now ships `thin` and `classic` SWUST Code logos. The selected value is stored as `logo_design`. The home screen also has a starry background with meteor animation, disabled automatically in plain-terminal mode to avoid rendering issues.

The default theme registry includes the `swust-code` theme name, with a blue primary color, cyan secondary color, and purple accent.

## Next-Prompt Prediction

When a session becomes idle, the TUI calls `POST /session/{sessionID}/predict` to generate a ghost suggestion for the next prompt:

- Shown only when the input is empty
- `Tab` accepts it
- `Esc` dismisses it
- Typing, status changes, or session switches clear it

Disable it in config:

```json
{
  "experimental": {
    "predict_next_prompt": false
  }
}
```
