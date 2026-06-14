# Goal-Driven Autonomy

Set a target with `--goal` and the run loop checks it when the agent tries to stop. v0.3 wires the independent LLM Judge into the core runner: it reads the transcript, tool results, and goal condition, then returns a structured verdict.

## Usage

```bash
swust-code run --goal "fix all TypeScript errors" "start working"
```

## Flow

1. User sets a goal with `--goal`
2. Agent runs normal tool calls
3. Goal Gate triggers when the agent is ready to stop
4. The runner builds a transcript and resolves the current model
5. Goal Judge calls `LLM.generateObject()` for `{ ok, impossible, reason }`
6. If not satisfied, a synthetic reminder is published and the agent continues
7. If satisfied or impossible, the goal is cleared and the run stops

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

`taskGate()` can still force continuation for non-terminal tasks. The current core runner still passes an empty task list, so wiring real `todowrite` state remains pending.
