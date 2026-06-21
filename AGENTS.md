# Documentation Editing Rules

This repository is the public documentation site for SWUST Code / 龙山灵码. Treat it as product documentation, not as a work log.

## Required Style

- Write stable user-facing documentation.
- Keep tone concise, factual, and product-oriented.
- Prefer current capabilities, installation steps, configuration, feature behavior, and release notes.
- Write like a maintainer explaining a tool to another developer. Do not write like a product launch, investor memo, or generic AI marketing page.
- Use Chinese for root pages and English for pages under `en/`.
- Keep terminology consistent:
  - Chinese product name: `龙山灵码`
  - English product name: `SWUST Code`
  - CLI command: `swust-code`
  - Config directory: `.swust-code/`
  - Environment prefix: `SWUST_CODE_*`

## Writing Voice

Use MiMo-Code's README and long-horizon blog as the closest style reference:

- Start with what the tool is and what it can do.
- Explain the concrete problem before explaining the design.
- Use commands, file paths, config keys, tables, and short lists as evidence.
- Keep feature descriptions tied to behavior users can observe.
- Put deeper technical reasoning in the right page, not on the homepage.

Use GitHub Docs and MDN-style technical writing as the default editorial model:

- Write for the user's next action.
- Prefer short paragraphs and clear headings.
- Make pages easy to scan before they are read end to end.
- Use the active voice.
- State limitations directly.

Good documentation should feel calm, specific, and useful. It should not feel like an AI-generated summary of a product strategy.

## Reference Sites

Before changing the home page or a long-form explanatory page, use these reference patterns:

- MiMo Code product page: short product name, one sentence, install command, primary links, then feature sections. Do not front-load a long theory of the project.
- MiMo Code long-horizon article: date, title, problem, design, mechanism, evaluation or limits, usage. Long pages should read like a technical note, not like a launch announcement.
- Radar project board: visual interest comes from information. Metrics, tags, source links, update dates, and ranked lists are useful. Decorative panels that do not carry facts are not useful.

Do not copy another site's visual identity, colors, imagery, or layout gimmicks. Extract the structure:

- one clear first action
- a compact fact panel
- visible commands or file paths
- short headings that describe the user's next decision
- evidence before claims

## Anti-AI Writing Rules

Before adding or rewriting any page, remove these patterns:

- Abstract praise without a concrete behavior: "更强大", "更智能", "全面升级", "极致体验", "创新闭环", "赋能开发者".
- Repeated product-name padding: do not start every paragraph with `龙山灵码` or `SWUST Code`.
- Grand claims that no user can verify from the page.
- Paragraphs that only rearrange buzzwords such as "长期任务", "工程治理", "智能体协作", "闭环", "演进".
- Fake balance phrases such as "不是简单的 X，而是 Y" unless the next sentence gives a real command, file, or behavior.
- Over-explaining history when the user came for setup, usage, or reference.

Replace them with concrete wording:

```md
Bad:
龙山灵码通过创新的长期任务闭环，全面提升真实工程场景下的智能体协作效率。

Good:
使用 `/goal` 设置停止条件。会话接近上下文上限时，checkpoint writer 会写入 `checkpoint.md`，恢复时再把 checkpoint、项目记忆和最近消息组合回上下文。
```

```md
Bad:
SWUST 层带来更完整、更先进的工程防护能力。

Good:
SWUST 层增加 Task Gate、Bash Safety 和 Write Guard。它们分别处理提前停止、高风险 shell 命令和越界写入。
```

## Page Structure Rules

Each page should have one job.

- Home page: say what SWUST Code is, who should use it, and where to go next. Keep it short.
- Quick start: installation, first run, provider setup, common commands, next links.
- Feature page: problem, behavior, commands/config, when to use it, limits.
- Reference page: exact syntax, fields, defaults, examples.
- Status page: stable current state only.
- Advantages page: explain differences with concrete behavior, not broad claims.
- Technical article page: start from the problem, then describe the design, implementation surface, limits, and usage.

When writing a feature page, use this order unless there is a strong reason not to:

1. What problem this feature solves.
2. What the user can do with it.
3. What commands, files, or config keys are involved.
4. When to use it.
5. What it does not do.

## Sentence-Level Rules

- Prefer one idea per sentence.
- Prefer "does X" over "is capable of X".
- Prefer "use `/subagent` to set a model for a visible subagent" over "supports personalized subagent governance".
- Prefer "writes `MEMORY.md`" over "implements durable knowledge persistence".
- Use English technical terms when they are product terms: `checkpoint`, `subagent`, `provider`, `variant`.
- Do not translate provider/model names.
- Do not invent slogans.
- Avoid defensive framing such as "不是 X，而是 Y" unless the next sentence gives a concrete command, file path, config field, or runtime behavior.
- If the page compares SWUST with MiMo, use tables and observable behavior instead of adjectives.

If a sentence would still sound plausible after replacing the product name with any other AI coding tool, rewrite it.

## Visual Design Rules

The docs site can be visually distinctive, but decoration must carry information.

- Prefer information panels, compact stat rows, tables, tags, command blocks, and source links.
- Use sharp borders, restrained spacing, and a small number of accent colors.
- Avoid large blurred gradients, abstract glow cards, fake dashboards, and ornamental terminal panels.
- Do not add a visual section unless it helps the user decide what to read, install, configure, or verify.
- Keep homepage density moderate. A developer should understand the product, install path, base relationship, and next pages without scrolling through repeated feature cards.

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

## Editorial Self-Check

Before committing a documentation change, read the changed page once and answer:

- Does the first screen tell the user what they can do next?
- Does every claimed advantage point to a command, file, config field, runtime behavior, or explicit limitation?
- Can a developer scan the headings and still understand the page?
- Did you remove process notes, branch state, PR state, and local validation chatter?
- Did you remove generic AI phrasing?
- Did you avoid overstating SWUST-specific value when the behavior is inherited from MiMo-Code?

If the answer to any item is "no", revise before committing.

## Verification

Before committing documentation changes, run:

```bash
bun run docs:build
```

Also scan for internal-process terms before pushing:

```bash
rg -n "PR #|Mergeable|mimo-rebase|pr/mimo|preview build|commit [0-9a-f]{7}" --glob '!bun.lock' --glob '!AGENTS.md'
```
