# Workflow Engine

v0.3 workflow runtime can execute scripts and orchestrate agents through explicit host functions. The current backend is a restricted host-function runner. QuickJS remains a possible future execution boundary.

## Runtime Model

`Workflow.Service` currently provides:

| Method | Description |
|--------|-------------|
| `start(input)` | Starts a workflow and immediately returns a `running` record |
| `getStatus(runID)` | Reads run status |
| `cancel(runID)` | Cancels through `AbortController` |
| `getJournal(runID)` | Reads the in-memory journal |

Statuses include `pending`, `running`, `completed`, `failed`, and `cancelled`. Thrown script errors mark the run as `failed`; cancellation marks it as `cancelled`.

## Script Example

```javascript
export const meta = {
  name: 'my-workflow',
  description: 'Custom workflow',
  phases: [{ title: 'Plan' }],
}

phase('Plan')
log('planning')

const result = await agent('summarize the plan', {
  label: 'planner',
  phase: 'Plan',
})

return { ok: true, text: result.text }
```

The runtime parses `meta`, records the name and phase, and injects host functions into the script scope.

## Host Functions

| Function | Current behavior |
|----------|------------------|
| `agent(prompt, opts?)` | Spawns an ephemeral subagent through Actor Spawn and records counters/results |
| `parallel(thunks)` | Runs tasks in parallel; agent calls are bounded by `maxConcurrentAgents` |
| `pipeline(items, ...stages)` | Processes item arrays through stages |
| `phase(title)` | Updates current phase and writes journal entries |
| `log(message)` | Writes journal entries |
| `workflow(name, args?)` | Calls a built-in workflow with depth limit 8 and cycle detection |

Scripts cannot access module loading or host globals such as `process`, `Bun`, `Deno`, `fetch`, `eval`, or `Function`.

## Journal And Resume

The workflow runtime maintains both an in-memory journal and disk JSONL:

| File | Purpose |
|------|---------|
| `<data>/workflow/<runID>.jsonl` | Records phase, log, agent result, and error events |
| `<data>/workflow/<runID>.js` | Saves script content for change detection |

Agent calls use `sha256(prompt + agentType + model + schema + phase)` to build deterministic keys. Resume replays completed results. If the script content changes, the old journal is cleared to avoid stale replay.

## Built-In Workflow

The built-in registry currently includes `deep-research`, with Plan, Search, Extract, Group, Crosscheck, and Report phases. It can be invoked from another script with `workflow("deep-research", args)`.
