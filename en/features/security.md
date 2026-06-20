# Security

SWUST Code uses a layered safety model shaped for real engineering work. It inherits the MiMo permission runtime and adds SWUST-specific safeguards where long tasks tend to fail in practice.

## Core Principles

The current mainline follows three practical principles:

- risky actions should default toward restriction, not silent allowance
- engineering risk should be recognized before execution when possible
- premature stopping, bad writes, and dangerous shell execution are first-class problems in long-running work

That is why SWUST looks at permissions, shell execution, write boundaries, task stopping conditions, and structured-document handling together.

## Safeguard Layers

| Layer | Main purpose |
|-------|--------------|
| permission pipeline | decide whether a tool call is allowed, asked, or denied |
| Bash Safety | analyze risky shell patterns before execution |
| Task Gate | reduce premature completion while unfinished tasks still exist |
| Write Guard | narrow writable paths and memory-write boundaries |
| Document Validation | add extra constraints for structured-document work |
| context governance | reduce drift through cache-stable context layout choices |

The permission runtime mostly comes from the MiMo base. Task Gate, Bash Safety, Write Guard, and Document Validation are more SWUST-specific engineering additions.

## Permission Pipeline

Tool calls do not execute immediately. They pass through a decision path:

1. blanket deny rules can reject immediately
2. blanket ask rules can require confirmation
3. the tool's own `checkPermissions()` can apply extra logic
4. the current mode can override the default path

This prevents file reads, edits, shell execution, and external access from being treated as if they carried the same risk.

## Bash Safety

Shell access is a major productivity feature and one of the main risk surfaces. Bash Safety adds extra attention to patterns such as:

- dangerous deletion
- download-and-execute behavior
- risky permission changes
- force reset or force push paths
- other operations that can create hard-to-reverse damage

The goal is not to block useful shell work. The goal is to reduce the category of commands that an agent should clearly not run casually.

## Task Gate And Write Guard

These two layers matter especially for long-running tasks:

- Task Gate asks whether the task is actually done
- Write Guard asks whether the target location should really be writable

The first reduces optimistic stopping. The second reduces out-of-bounds edits, bad memory writes, and inappropriate directory mutations.

## Why This Matters More In Long Tasks

In a short task, a mistake may only affect one response. In a long task, mistakes accumulate into broken state:

- one bad write can pollute later steps
- one premature stop can break continuity
- one unsafe shell action can affect the whole repository
- one incorrect document edit can distort later automation

SWUST includes these layers in the mainline because it is designed for long-running engineering work, not just one-turn prompting.
