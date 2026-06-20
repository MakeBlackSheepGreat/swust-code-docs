# Documentation Editing Rules

This repository is the public documentation site for SWUST Code / 龙山灵码. Treat it as product documentation, not as a work log.

## Required Style

- Write stable user-facing documentation.
- Keep tone concise, factual, and product-oriented.
- Prefer current capabilities, installation steps, configuration, feature behavior, and release notes.
- Use Chinese for root pages and English for pages under `en/`.
- Keep terminology consistent:
  - Chinese product name: `龙山灵码`
  - English product name: `SWUST Code`
  - CLI command: `swust-code`
  - Config directory: `.swust-code/`
  - Environment prefix: `SWUST_CODE_*`

## Do Not Add Internal Process Details

Do not put temporary engineering status into public docs, including:

- PR status, mergeability, branch names, or bridge-branch explanations.
- Commit hashes unless documenting a developer-only troubleshooting case.
- Local preview build versions.
- CI run summaries such as exact task counts.
- Agent session notes, migration scratch notes, or "what I just did" summaries.
- Speculation about future merge strategy.

If project status must be documented, write it as stable state, for example:

```md
Current version: v0.6.0
The mainline uses MiMo-Code as its runtime base.
```

Avoid process-log wording such as open pull-request status, mergeability notes, local preview versions, temporary branch names, or raw commit identifiers in user-facing docs.

## MiMo-Code Base Principle

SWUST Code v0.5.0+ is based on MiMo-Code. When describing implementation:

- If MiMo-Code already provides a capability, describe it as inherited from the MiMo-Code base.
- Only describe SWUST Code as adding behavior when the capability is actually SWUST-specific.
- Keep provider and model names unchanged: `MiMo Auto`, Xiaomi MiMo Platform, `mimo/mimo-auto`, and `xiaomi/mimo-*` are provider/model names, not product branding to replace.
- Do not imply the project is reverting to OpenCode. OpenCode references should be historical unless explicitly comparing older versions.

## Changelog Rules

- Changelog entries should describe release-level changes.
- Do not create separate entries for temporary PR syncs, local validation notes, or branch housekeeping.
- Fold follow-up fixes for the same release into the release section when appropriate.
- Use semantic versions such as `v0.6.0`.

## Navigation And Home Page Rules

- Home page content should guide users to core product documentation.
- Do not add prominent homepage features for internal migration status.
- Navigation should prioritize Guide, Features, API, Dev, Changelog, and GitHub.
- Status pages may exist for compatibility, but they must describe stable current state rather than temporary workflow.

## Verification

Before committing documentation changes, run:

```bash
bun run docs:build
```

Also scan for internal-process terms before pushing:

```bash
rg -n "PR #|Mergeable|mimo-rebase|pr/mimo|preview build|commit [0-9a-f]{7}" --glob '!bun.lock' --glob '!AGENTS.md'
```
