# Workflow Engine

The workflow module is the runtime scaffold for scriptable multi-agent orchestration.

Current status: `packages/opencode/src/workflow/runtime.ts` defines workflow run records, status lookup, cancellation, metadata parsing, an in-memory journal structure, and concurrency/lifecycle constants. Script execution, host-function injection, subagent spawning, the QuickJS sandbox, and persistent crash recovery are pending. Today `start()` parses `meta` and then immediately marks the run as `completed`.

## Runtime Model

The runtime currently tracks:

| Field | Description |
|-------|-------------|
| `runID` | Workflow run ID |
| `sessionID` | Associated session |
| `status` | `pending`, `running`, `completed`, `failed`, or `cancelled` |
| `name` | Parsed from `meta.name` |
| `currentPhase` | Initialized from `meta.phases[0].title` |
| Agent counters | Fields exist; live counter updates depend on future script execution wiring |

## Metadata

The current parser reads simple `export const meta = { ... }` blocks:

```javascript
export const meta = {
  name: 'my-workflow',
  description: 'Custom workflow',
  phases: [{ title: 'Phase 1' }],
}
```

When parsing succeeds, `name` and the first phase are copied into the run record.

## Reserved Host Functions

The type layer defines these host functions:

| Function | Intended use |
|----------|--------------|
| `agent(prompt, opts?)` | Spawn a subagent |
| `parallel(thunks)` | Run tasks concurrently |
| `pipeline(items, ...stages)` | Process items through stages |
| `phase(title)` | Mark a phase |
| `log(message)` | Write a log entry |
| `workflow(name, args?)` | Call another workflow |

These functions are not injected into an executable sandbox yet.

## Journal

`WorkflowJournal` is currently an in-memory structure. It can append `phase`, `agent_start`, `agent_complete`, `agent_fail`, `log`, and `error` events, and read the last phase.

Persistent JSONL, script hash validation, and checkpoint resume are still pending.
