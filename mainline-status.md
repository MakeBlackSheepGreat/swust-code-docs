# 主线状态

> 更新日期：2026-06-20  
> 代码仓库：<https://github.com/MakeBlackSheepGreat/swust-code>  
> 当前声明版本：v0.5.0

## 当前定位

龙山灵码（SWUST Code）当前主线以 MiMo-Code 为运行时基座。项目保留 SWUST Code 的品牌、中文体验和工程化增强，但不把 MiMo-Code 已有能力重写成旧 OpenCode 风格。

维护原则：

| 场景 | 处理方式 |
|------|----------|
| MiMo-Code 已经提供能力 | 以 MiMo-Code 原生实现为准 |
| MiMo-Code 没有该能力 | 以最小改动叠加 SWUST 层实现 |
| Provider 或模型名称 | 保持服务商原名，不做品牌替换 |
| 旧 SWUST Code 与 MiMo-Code 行为冲突 | 优先保留 MiMo-Code 行为 |

## 当前能力边界

MiMo-Code 基座提供：

- 终端 TUI、server runtime、Web / Desktop 入口
- 多 Provider 模型路由和 OpenAI 兼容接入
- LSP、MCP、插件、自定义命令、技能系统
- 持久化记忆、checkpoint、上下文重建
- actor / subagent 编排与任务追踪
- `goal`、`compose`、Dream / Distill、语音输入

SWUST 层补充：

- 龙山灵码品牌与中文本地化
- 更完整的 TUI 侧边栏上下文和 Getting Started 提示
- attention 通知与声音包配置
- Task Gate、Bash Safety、Write Guard
- Document Validation、cache-stable 上下文布局
- `@path` 记忆导入与 one-fact-per-file 事实存储
- `/memory`、`/paste-image` 和常用 TUI 控件别名

## TUI 状态

当前主线保留 MiMo/OpenTUI 的终端体验，同时迁移旧 SWUST Code 较好的侧边栏组织方式。侧边栏覆盖工作目录、指令文件、Goal、Task、Todo、LSP、MCP、变更文件、上下文窗口、token、费用和缓存指标。

首页 Logo 已调整为 SWUST Code 深蓝主色；侧边栏颜色保持接近旧 SWUST Code 的阅读体验。

## Provider 命名

这些名称是服务商或模型 ID，不属于 SWUST 品牌替换范围：

- `MiMo Auto`
- `小米 MiMo 平台`
- `mimo/mimo-auto`
- `xiaomi/mimo-*`

## 验证状态

当前主线在最近一次推送前已完成针对 CLI 包的 TypeScript 类型检查和命令相关测试。正式发布前仍建议执行完整构建、完整测试、release 和 npm publish 验证。

## 文档维护要求

文档只描述稳定的当前能力和用户可执行路径。临时分支、PR 状态、本地构建记录、commit hash 和 Agent 会话过程不应写入公开文档。
