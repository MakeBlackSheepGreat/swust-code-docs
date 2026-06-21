---
layout: home

hero:
  name: 龙山灵码
  text: "SWUST Code"
  tagline: "基于 MiMo-Code 的终端 AI 编程工具，适合在真实仓库中处理修复、重构、迁移等需要多轮推进的任务。"
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
    <p class="swust-kicker">安装</p>
    <pre><code>npm install -g @swust-code/cli
swust-code</code></pre>
  </div>
  <div class="swust-facts">
    <p class="swust-kicker">信息</p>
    <dl>
      <div><dt>版本</dt><dd>v0.6.0</dd></div>
      <div><dt>基座</dt><dd>MiMo-Code</dd></div>
      <div><dt>命令</dt><dd><code>swust-code</code></dd></div>
      <div><dt>项目资产</dt><dd><code>.swust-code/</code></dd></div>
    </dl>
  </div>
</section>

## 适合处理的任务

龙山灵码更适合放在已有仓库里使用，尤其是一次对话很难完成的工作：

- 修复一组测试、类型或构建错误
- 分阶段完成重构、迁移或功能实现
- 把调查、实现、评审、验证交给不同子智能体
- 在多次会话之间保留项目规则、结论和进度

如果只是解释一个概念，普通聊天工具通常更直接。

## 核心能力

### 记住项目上下文

项目记忆保存长期规则和事实。会话接近上下文上限时，checkpoint 会记录当前进度，恢复时再把必要信息组合回上下文。

阅读：[持久化记忆](/features/memory)

### 拆分长任务

`goal` 用自然语言描述完成条件，`compose` 用于组织复杂任务，subagent 用于处理局部调查、实现或验证。

阅读：[智能体模式](/features/agents)

### 收紧工程风险

Task Gate、Bash Safety、Write Guard 和 Document Validation 分别处理提前停止、高风险 shell 命令、越界写入和结构化文档修改。

阅读：[安全防护](/features/security)

### 沉淀重复流程

`/dream` 用于整理项目知识，`/distill` 用于把重复动作沉淀为 skill、command、subagent 或 workflow。

阅读：[工作流引擎](/features/workflow)

## 从这里开始

| 目标 | 页面 |
|------|------|
| 安装并完成第一次启动 | [快速开始](/guide/start) |
| 配置模型和 Provider | [LLM 提供商](/guide/providers) |
| 了解子智能体、`goal` 和 `compose` | [智能体模式](/features/agents) |
| 查看 CLI 和配置字段 | [CLI 命令](/api/commands)、[配置 Schema](/api/config-schema) |
| 了解当前版本状态 | [主线状态](/mainline-status) |
