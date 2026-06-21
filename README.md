# 龙山灵码文档站

This repository contains the VitePress documentation site for [SWUST Code / 龙山灵码](https://github.com/MakeBlackSheepGreat/swust-code).

## Development

```bash
bun install
bun run docs:dev
```

## Build

```bash
bun run docs:build
```

## Deploy

Cloudflare Pages deploys the site automatically when `main` is pushed.

## Structure

```text
index.md              # Chinese homepage
en/index.md           # English homepage
guide/                # Getting started guides
features/             # Feature documentation
api/                  # CLI, tools, HTTP API, config schema
dev/                  # Developer documentation
mainline-status.md    # Stable current mainline status
changelog.md          # Release-level changelog
.vitepress/config.ts  # VitePress configuration
```
