# Goal-Driven Autonomy

Set a goal with `--goal` so the run loop checks the target when the agent tries to stop. The current code has Goal Store, Goal Gate, and a 12 re-entry cap. Full independent LLM Judge integration is still pending.

## Usage

```bash
swust-code run --goal "fix all TypeScript errors" "start working"
```

## How It Works

1. User sets a goal
2. Agent begins working
3. When agent tries to stop, **Goal Gate** triggers
4. Goal Gate calls an evaluator
5. If goal not met: injects synthetic message, agent continues
6. If goal met or impossible: stops normally

## Goal Judge

The intended evaluator returns `{ ok, impossible, reason }`.

- `ok=true` clears the goal and stops
- `impossible=true` clears the goal and stops
- Otherwise the loop injects a `<system-reminder>` and continues

In the current core runner, the evaluator is still a placeholder returning `Judge not yet integrated`. The `--goal` option exists, but the final judgment quality depends on the pending Judge wiring.

## Re-entry Control

| Role | Max Re-entries |
|------|---------------|
| Main Agent | 12 |

## Task Gate

`taskGate()` can force continuation when non-terminal tasks exist. The current runner still passes an empty task list, so wiring real todowrite state remains pending.
