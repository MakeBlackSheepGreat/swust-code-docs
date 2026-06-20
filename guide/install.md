# 安装

## npm 安装（推荐）

```bash
npm install -g @swust-code/cli
```

## 从源码构建

```bash
git clone https://github.com/MakeBlackSheepGreat/swust-code.git
cd swust-code
bun install
bun run --cwd packages/opencode src/index.ts
```

开发模式也可以使用仓库根目录脚本：

```bash
bun run dev
```

## 系统要求

- **Bun** 1.3.11（源码运行和构建使用 Bun）
- **Node.js** 18+（部分生态工具仍会用到）
- **操作系统** macOS / Linux / Windows（PowerShell、Git Bash 或 WSL 均可）
- **内存** 4GB+ 推荐

## 验证安装

```bash
swust-code --version
swust-code --help
```
