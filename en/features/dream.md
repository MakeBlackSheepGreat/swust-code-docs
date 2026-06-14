# Self-Improvement

v0.3 turns Dream and Distill from explanatory commands into runnable autonomous tasks. Both commands reuse `runAutonomyTask()` and launch `swust-code run` with `--goal`, letting the primary agent perform memory consolidation or workflow packaging.

## Dream

```bash
swust-code dream
```

Options:

| Option | Description |
|--------|-------------|
| `--dry-run` | Show the task text without starting an agent |
| `--yes`, `-y` | Skip confirmation |
| `--model`, `-m` | Select a `provider/model` |
| `--agent` | Select the primary agent |
| `--dir` | Run against a project directory |

Dream starts an autonomous run titled `Auto Dream`. Its goal is to consolidate verified durable project knowledge into SWUST Code memory.

Task constraints:

1. Use memory files as the working index
2. Use the raw trajectory database as the source of truth
3. Use read-only SQLite and filesystem inspection
4. Write only durable, verified information

## Distill

```bash
swust-code distill
```

Distill starts an autonomous run titled `Auto Distill`. Its goal is to identify repeated workflows and create only high-confidence missing skills, agents, or commands.

Task constraints:

1. Review the past month of sessions
2. Verify repeated manual workflows against the trajectory database
3. Inventory existing skills, agents, and commands first
4. Produce a compact shortlist
5. Create only missing assets with clear value

## Auto Trigger

After a normal session finishes, the core runner tries to load `session/auto-dream.ts` and queues the relevant command in the background when conditions are met.

| Task | Interval | Background command |
|------|----------|--------------------|
| Dream | 7 days | `swust-code dream --yes --dir <cwd>` |
| Distill | 30 days | `swust-code distill --yes --dir <cwd>` |

Trigger conditions:

- `SWUST_CODE_AUTO_EVOLUTION` is not `0` or `false`
- The last same-title run is older than the interval
- The project has enough session history
- At least 10 seconds have passed since the last spawn

The child process receives `SWUST_CODE_AUTO_EVOLUTION=0` to prevent recursive auto-triggering.
