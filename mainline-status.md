# 项目状态

> 更新时间：2026-06-20  
> 代码仓库：<https://github.com/MakeBlackSheepGreat/swust-code>  
> 当前版本：v0.5.0

## 当前定位

龙山灵码（SWUST Code）当前主线已经切换到 MiMo-Code 基座。项目保留 SWUST Code 的品牌、中文体验和工程化增强，同时以 MiMo-Code 的原生能力作为运行时基础。

## 主线能力

- MiMo-Code 原生能力：持久化记忆、checkpoint、actor/subagent 编排、task、goal、Compose、Dream/Distill、语音输入、TUI、LSP、MCP 和插件系统。
- SWUST 增强能力：Task Gate、Bash Safety、Cache-Stable Prefix、`@path` 记忆导入、Fact Store、Write Guard 和 Document Validation。
- 品牌与路径：CLI 使用 `swust-code`，配置目录使用 `.swust-code/`，环境变量使用 `SWUST_CODE_*`。
- Provider 命名保持原样：`MiMo Auto`、小米 MiMo 平台、`mimo/mimo-auto`、`xiaomi/mimo-*` 仍作为服务商或模型名称使用。

## TUI 状态

新主线已经迁移旧 SWUST Code 侧边栏体验，包括工作目录、指令文件、Goal、Task、Todo、LSP、MCP、变更文件、上下文窗口、token、费用和缓存指标。Getting started 提示、路径显示、中文 i18n、attention 通知和声音包配置也已接入。

## 验证状态

当前主线在推送前通过了 TypeScript 类型检查。后续发布前仍建议按发布流程补跑完整测试、构建、release 和 npm publish 验证。

## 后续维护原则

- MiMo-Code 已有的能力以 MiMo-Code 实现为准。
- 旧 SWUST Code / OpenCode 中 MiMo-Code 没有的能力，按最小改动迁移。
- 文档以当前可用能力为准，不记录临时分支、提交 hash 或本地预览构建信息。
