# 主线状态

> 更新时间：2026-06-20  
> 代码仓库：<https://github.com/MakeBlackSheepGreat/swust-code>  
> 当前主线合入方式：PR [#1](https://github.com/MakeBlackSheepGreat/swust-code/pull/1)

## 当前结论

龙山灵码（SWUST Code）的 MiMo-Code 基座迁移分支已经进入可合入状态。由于旧 `main` 历史来自 OpenCode 基座，而新迁移分支来自 MiMo-Code 基座，两条历史没有共同 merge base，因此本次合入使用 bridge PR 分支：

| 项目 | 状态 |
|------|------|
| 目标分支 | `main` |
| 迁移分支 | `mimo-rebase` |
| PR 分支 | `pr/mimo-rebase-to-main` |
| PR 状态 | Open / Mergeable |
| 最新迁移提交 | `520db45 docs: rewrite swust code readme` |
| 代码内部包版本 | `0.1.1` |
| 当前本地预览构建版本 | `0.0.0-swust-code-rebrand-202606200248` |

bridge PR 分支的最终文件树与 `swust-code/mimo-rebase` 完全一致；第一父提交是旧 `main`，第二父提交是 `mimo-rebase`。这样 GitHub 可以正常创建和合并 PR，同时保留迁移分支的提交历史。

## 已完成内容

### MiMo-Code 基座迁移

- 基座切换到 MiMo-Code fork。
- 保留 MiMo-Code 原生能力：Provider/TUI/LSP/MCP/plugin、持久化记忆、checkpoint、actor/subagent、task、goal、Compose、Dream/Distill、voice。
- 品牌替换为 SWUST Code / 龙山灵码：包名、CLI、环境变量、配置目录、文档链接和界面文案已同步。
- AI 服务商名称保持原样：`MiMo Auto`、`小米 MiMo 平台`、`mimo/mimo-auto`、`xiaomi/mimo-*` 不做品牌替换。

### SWUST 增量能力

- Task Gate：主 agent 和合规 subagent 停止前检查未完成任务。
- Bash Safety：高风险 Bash 命令执行前安全分析。
- Cache-Stable Prefix：上下文前缀稳定化，提高 provider cache 命中率。
- Memory Import / Fact Store：`@path` 记忆导入、one-fact-per-file 项目事实存储。
- Write Guard：记忆与任务进度写入路径保护。
- Document Validation：面向 spec-driven 文件的文档结构验证。

### TUI 与文档体验

- 旧 SWUST Code 侧边栏体验已迁移到新 TUI：工作目录、指令文件、goal、task、todo、LSP、MCP、变更文件、上下文窗口、token、费用和缓存指标。
- `TuiPathsProvider` 已接入 TUI app runtime。
- Getting started 提示、路径显示和中文 i18n 已补齐。
- Attention 通知和声音包配置已接入。
- README / README.zh 已按旧 SWUST Code 风格重写，并修正为 MiMo-Code 基座表述。

## 验证记录

- 迁移分支推送前触发 `bun turbo typecheck`：12/12 tasks successful。
- PR 分支推送前再次触发 `bun turbo typecheck`：12/12 tasks successful。
- GitHub PR [#1](https://github.com/MakeBlackSheepGreat/swust-code/pull/1) 当前为 `MERGEABLE`。
- 本地提示：当前 Bun 为 `1.3.14`，仓库 `packageManager` 声明为 `bun@1.3.11`。

## 仍需跟进

- 合并 PR #1 到 `main` 后，确认自动部署、release 和 npm publish 流程。
- 如需正式发布，应设置 release channel，使构建版本使用 `packages/opencode/package.json` 的 `0.1.1`，而不是分支预览版本。
- 文档站仍需持续从新仓库 `packages/web/src/content/docs` 中回迁最新配置和 Provider 页面。

