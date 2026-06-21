---
layout: home

hero:
  name: 龙山灵码
  text: "SWUST Code"
  tagline: "基于 MiMo-Code 的终端 AI 编程工具。它保留 MiMo-Code 的长任务运行时，并在中文 TUI、工程防护、记忆组织和项目级子智能体配置上增加 SWUST 层。"
  actions:
    - theme: brand
      text: 快速开始
      link: /guide/start
    - theme: alt
      text: GitHub
      link: https://github.com/MakeBlackSheepGreat/swust-code
    - theme: alt
      text: NPM
      link: https://www.npmjs.com/package/@swust-code/cli
---

<section class="swust-home-intro">
  <div class="swust-install">
    <p class="swust-kicker">INSTALL</p>
    <pre><code>npm install -g @swust-code/cli
swust-code</code></pre>
  </div>
  <div class="swust-facts">
    <p class="swust-kicker">CURRENT LINE</p>
    <dl>
      <div><dt>声明版本</dt><dd>v0.6.0</dd></div>
      <div><dt>运行时基座</dt><dd>MiMo-Code</dd></div>
      <div><dt>CLI</dt><dd><code>swust-code</code></dd></div>
      <div><dt>项目目录</dt><dd><code>.swust-code/</code></dd></div>
    </dl>
  </div>
</section>

## 当前主线

| 模块 | 当前行为 |
|------|----------|
| MiMo-Code 基座 | memory、checkpoint、subagent、`goal`、`compose`、MCP、LSP 和插件能力继续遵循 MiMo 当前主线。 |
| 可恢复长任务 | `MEMORY.md`、facts、`checkpoint.md` 和 task progress 用于保存项目事实、会话状态和任务进度。 |
| subagent 设置 | 使用 `/subagent` 为可见子智能体设置模型、variant 和最大步数，配置写入项目 config。 |

## 先确认这三件事

| 问题 | 结论 | 继续阅读 |
|------|------|----------|
| 当前主线基于什么 | MiMo-Code。MiMo 已有能力优先保留原生实现。 | [主线状态](/mainline-status) |
| SWUST 新增什么 | 中文 TUI、Task Gate、Bash Safety、Write Guard、Document Validation、`/subagent` 项目级配置等。 | [SWUST 优势](/DIFFERENCES) |
| 第一次怎么用 | 安装 CLI，在仓库根目录运行 `swust-code`，按向导配置 Provider。 | [快速开始](/guide/start) |

## 适合什么工作

SWUST Code 更适合真实仓库里的连续任务：

- 多文件修复、重构、迁移、升级
- 需要 `goal` 判断完成条件的长任务
- 需要 subagent 调查、实现、评审或验证的任务
- 需要在多次会话之间保留项目规则、事实和进度的任务

如果只是问一个简短概念，普通聊天工具通常更直接。

## MiMo 基座与 SWUST 层

| 层级 | 内容 | 说明 |
|------|------|------|
| MiMo-Code 基座 | memory、checkpoint、actor / subagent、`goal`、`compose`、Dream / Distill、MCP、LSP、插件、TUI / Server Runtime | 文档中按 MiMo 原生能力描述。 |
| SWUST 层 | 中文优先信息组织、侧边栏体验、工程防护、记忆路径守卫、文档验证、子智能体项目级配置 | 只在 MiMo 没有或 SWUST 明确增强的地方写成新增价值。 |

## 常用入口

| 你要做什么 | 页面 |
|------------|------|
| 安装、首次启动、配置 Provider | [快速开始](/guide/start) |
| 理解主智能体、`goal`、`compose` 和 subagent | [智能体模式](/features/agents) |
| 理解 `MEMORY.md`、facts 和 checkpoint | [持久化记忆](/features/memory) |
| 查看 Task Gate、Bash Safety、Write Guard | [安全防护](/features/security) |
| 查看 CLI 命令和配置字段 | [CLI 命令](/api/commands)、[配置 Schema](/api/config-schema) |

## 命名边界

Provider 和模型名称不替换：

- `MiMo Auto`
- `小米 MiMo 平台`
- `mimo/mimo-auto`
- `xiaomi/mimo-*`

这些是服务商或模型标识，不是 SWUST 品牌文案。
