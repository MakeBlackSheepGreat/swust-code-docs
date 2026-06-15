# Goal-Driven Autonomy

Set a target with `--goal` and the run loop checks it when the agent tries to stop. Since v0.4, Goal is a dedicated agent mode: when `--agent` is omitted, `swust-code run --goal ...` routes to the `goal` agent and injects goal-specific prompts and reminders.

## Usage

```bash
swust-code run --goal "fix all TypeScript errors" "start working"
```

## Flow

1. User sets a goal with `--goal`
2. CLI selects the `goal` agent unless `--agent` is explicit
3. The agent runs normal tool calls
4. Goal Gate triggers when the agent is ready to stop
5. The runner builds a transcript and resolves the current model
6. Goal Judge calls `LLM.generateObject()` for `{ ok, impossible, reason }`
7. If not satisfied, a synthetic reminder is published and the agent continues
8. If satisfied or impossible, the goal is cleared and the run stops

## Goal Judge

The Judge uses a separate system prompt and is instructed to evaluate concrete evidence such as code changes, tests, file state, and tool output.

| Behavior | Current implementation |
|----------|------------------------|
| Output | `Verdict` schema: `ok`, `impossible`, `reason` |
| Sampling | `temperature: 0`, `maxTokens: 500` |
| Context | User text, assistant text, reasoning, tool success/error results, shell output, compaction summaries |
| Failure policy | If Judge evaluation fails, it returns not-satisfied and continues |

## Re-entry Control

| Role | Max Re-entries |
|------|---------------|
| Main Agent | 12 |

After the cap is exceeded, the goal is cleared to prevent an infinite loop.

## Task Gate

`taskGate()` can force continuation for non-terminal tasks. v0.4 also adds durable Task Registry and actor task binding, so task-oriented subagents can start, complete, or block tasks through the runtime.
