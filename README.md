# 龙山灵码 Documentation

Documentation site for 龙山灵码 ([SWUST Code](https://github.com/MakeBlackSheepGreat/swust-code)), built with VitePress.

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

Deployed to Cloudflare Pages automatically on push to `main`.

## Structure

```
├── index.md              # Chinese homepage
├── en/index.md           # English homepage
├── guide/                # Getting started guides
├── features/             # Feature documentation
│   └── tui.md            # TUI experience and interaction polish
├── api/                  # API reference, including CLI and HTTP API
├── dev/                  # Developer documentation
├── changelog.md          # Changelog
├── DIFFERENCES.md        # Comparison with OpenCode
└── .vitepress/config.ts  # VitePress configuration
```
