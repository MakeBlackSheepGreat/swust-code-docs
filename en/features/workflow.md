# Workflow Engine

SWUST Code's workflow engine turns multi-agent work into a recoverable, inspectable, repeatable engineering process. It is not just a command alias layer. It is an orchestration runtime for long tasks.

## What Problem It Solves

Workflow becomes more appropriate than a single conversational thread when the task:

- needs explicit stages
- needs multiple subagents
- needs intermediate records
- needs resume behavior after interruption
- needs to be repeated more than once

In those cases, the workflow engine makes the process itself part of the system rather than leaving it implicit in the conversation.

## How It Relates To `compose`, `goal`, And Subagents

| Capability | Better suited for |
|------------|-------------------|
| `compose` | giving a complex task structure from within the primary agent |
| `goal` | continuing until a stop condition is truly satisfied |
| subagents | handing local units of work to separate roles |
| workflow | turning the whole multi-stage process into a scripted, resumable run |

Workflow is the most explicit orchestration layer among them.

## Runtime Model

Workflow scripts run in a restricted environment and use explicit host functions:

| Function | Purpose |
|----------|---------|
| `agent(prompt, opts?)` | spawn a subagent for one task unit |
| `parallel(thunks)` | run tasks concurrently |
| `pipeline(items, ...stages)` | process a set of items through stages |
| `phase(title)` | mark the current stage |
| `log(message)` | write structured run output |
| `workflow(name, args?)` | call a built-in or saved workflow |

The point of the restricted environment is to keep execution boundaries clearer and recovery behavior more predictable.

## Journal And Resume

The workflow engine records execution instead of treating every run as an unrepeatable transient action.

Typical persisted state includes:

- current phase
- important logs
- subagent outputs
- error events
- script content and run identity

That makes it easier to decide whether a workflow should resume, continue, or restart cleanly.

## Built-In Workflows

The current mainline already includes built-in workflows such as `deep-research`. They are useful when search, extraction, grouping, cross-checking, and reporting should be kept as separate phases instead of being compressed into one conversational turn.

The real value of workflow is not that the script looks advanced. The value is that the process stays understandable as the task grows.

## When To Switch To Workflow

Workflow is usually worth it when:

- the task will be repeated
- research, implementation, review, and verification should be separated clearly
- multiple subagents need coordinated execution
- intermediate results must survive interruption

For a small one-off task, the primary agent or `compose` is usually lighter.
