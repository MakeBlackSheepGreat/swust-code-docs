# Architecture

SWUST Code is organized around terminal interfaces, task orchestration, session runtime, tools, and project-state storage. A useful first pass is to read the system by responsibility rather than by exact source directory.

## Runtime Layers

```text
Interface Layer
  CLI / TUI / Web / Desktop / API server

Extension Layer
  Plugins / Skills / MCP / custom commands / integration surfaces

Coordination Layer
  Agent orchestration / subagents / workflow / goal / compose

Execution Layer
  Session runtime / tool registry / permissions / model routing / context rebuild

Foundation Layer
  Effect services / SQLite + Drizzle / config / filesystem / project state
```

This diagram describes responsibility boundaries. It does not map one-to-one to every source directory.

## Monorepo Areas

| Package group | Main responsibility |
|---------------|---------------------|
| `opencode` | runtime, CLI, sessions, tools, config, server routes |
| `app` / `desktop` / `web` / `console` | user interfaces and interaction surfaces |
| `sdk` / `ui` / `shared` | shared types, components, and common utilities |
| `plugin` / `extensions` / `function` | extension and runtime integration surfaces |
| `script` / `containers` / `identity` / `enterprise` / `slack` / `storybook` | build, integration, deployment, and surrounding services |

## Critical Paths

### Session Runtime

The session runtime assembles input, selects models, calls tools, handles permissions, and records messages. Long tasks also use memory, checkpoints, and context reconstruction.

### Agent Orchestration

The primary agent, subagents, `goal`, `compose`, and workflows share task state and tool boundaries. Subagent results return to the primary task path, while workflows make multi-stage execution resumable.

### Engineering Safeguards

Task Gate, Bash Safety, Write Guard, and Document Validation affect execution boundaries. They handle premature stopping, risky shell commands, write targets, and structured-document edits.

## Reading Order

To continue into the code structure, start with:

1. [Agent Modes](/en/features/agents)
2. [Persistent Memory](/en/features/memory)
3. [Workflow Engine](/en/features/workflow)
4. [Security](/en/features/security)
5. [Config Schema](/en/api/config-schema)
