# Self-Improvement

SWUST Code learns from your usage patterns and continuously improves.

## Dream (Knowledge Consolidation)

```bash
swust-code dream
```

Current status: the `dream` CLI command, dedicated agent prompt, and 7-day interval check exist. The automatic trigger currently returns false until it is wired into the session lifecycle, so run the command manually for now.

## Distill (Skill Discovery)

```bash
swust-code distill
```

Current status: the `distill` CLI command, dedicated agent prompt, and 30-day interval check exist. The CLI handler is still a prompt-style stub and the full subagent orchestration is marked as a later phase.

## Auto-Trigger Mechanism

| Task | Interval | Check Condition |
|------|----------|-----------------|
| Dream | 7 days | Last Dream session time |
| Distill | 30 days | Last Distill session time |

Implementation notes:
- `session/auto-dream.ts` defines intervals, titles, and task text
- `shouldAutoDream()` and `shouldAutoDistill()` currently return false
- `dream` shows the consolidation flow and asks for confirmation
- `distill` explains workflow packaging, then reports that full orchestration is pending
