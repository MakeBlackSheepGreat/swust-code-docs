# Installation

## npm (recommended)

```bash
npm install -g swust-code
```

## From Source

```bash
git clone https://github.com/MakeBlackSheepGreat/swust-code.git
cd swust-code
bun install
bun run --cwd packages/opencode src/index.ts
```

For local development from the repository root:

```bash
bun run dev
```

## Requirements

- **Bun** 1.3.14 for source development and builds
- **Node.js** 18+ for ecosystem tooling
- **OS** macOS / Linux / Windows with PowerShell, Git Bash, or WSL
- **Memory** 4GB+ recommended

## Verify

```bash
swust-code --version
swust-code --help
```
