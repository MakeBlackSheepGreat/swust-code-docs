---
layout: home

hero:
  name: 龙山灵码
  text: "基于 MiMo-Code 的终端原生 AI 编程智能体"
  tagline: "在终端里推进真实仓库工作：读代码、改文件、跑命令、拆给子智能体、写 checkpoint，并把项目知识留到下一次会话。"
  actions:
    - theme: brand
      text: 快速开始
      link: /guide/start
    - theme: alt
      text: SWUST 优势
      link: /DIFFERENCES
    - theme: alt
      text: 主线状态
      link: /mainline-status

features:
  - title: 长任务连续性
    details: "记忆、checkpoint、任务进度和上下文重建一起工作。恢复会话时，Agent 不需要从头理解仓库。"
    link: /features/memory
  - title: 多智能体协作
    details: "build、plan、compose、goal 与 subagent 共享运行时。规划、执行、评审和验证可以放在一条任务链里。"
    link: /features/agents
  - title: 工程防护
    details: "Task Gate、Bash Safety、Write Guard 和 Document Validation 处理提前停止、危险命令、越界写入和结构化文档错误。"
    link: /features/security
  - title: 中文优先 TUI
    details: "侧边栏、命令别名、提示反馈和主题按中文开发者的日常终端使用重新整理。"
    link: /features/tui
  - title: 可演进的项目知识
    details: "/dream 整理长期知识，/distill 把重复工作流沉淀为 skill、command、subagent 或 workflow。"
    link: /features/dream
  - title: 子智能体个性化
    details: "/subagent 为可见子智能体设置项目级模型、思考强度和最大步数。"
    link: /features/agents
---

<div class="swust-signal-row">
  <a class="swust-signal" href="/mainline-status">
    <span class="swust-signal-label">当前主线</span>
    <strong>MiMo-Code 基座</strong>
    <span>v0.6.0</span>
  </a>
  <a class="swust-signal" href="/features/agents">
    <span class="swust-signal-label">智能体</span>
    <strong>build / plan / compose / goal</strong>
    <span>subagent 可项目级配置</span>
  </a>
  <a class="swust-signal" href="/features/memory">
    <span class="swust-signal-label">连续性</span>
    <strong>memory + checkpoint</strong>
    <span>恢复、压缩、重建上下文</span>
  </a>
</div>

<div class="swust-terminal">
  <div class="swust-terminal-bar">
    <span></span><span></span><span></span>
    <strong>swust-code</strong>
  </div>
  <div class="swust-terminal-body">

```bash
$ swust-code
> /goal 修复类型错误并更新测试
> /subagent
> /dream
```

  </div>
</div>

## 产品定位

龙山灵码（SWUST Code）不是把终端聊天助手包装成“会写代码”的工具，而是把 **长期上下文、目标驱动自治、子智能体协作和工程防护** 放在同一条运行时路径上。它适合需要多轮推进的软件工程任务，例如：

- 在现有仓库中持续推进修复、重构、升级改造或验证
- 需要跨多个文件、多个工具、多个阶段协作的开发任务
- 希望 Agent 能在恢复会话后继续工作，而不是从头理解项目
- 需要把项目规则、架构知识和重复工作流逐步沉淀下来

## 为什么先看这几个页面

| 页面 | 适合什么时候看 |
|------|----------------|
| [快速开始](/guide/start) | 第一次安装、首次配置 Provider、理解常用命令 |
| [主线状态](/mainline-status) | 想确认当前主线基于什么、继承了什么、SWUST 额外加了什么 |
| [SWUST 优势](/DIFFERENCES) | 想理解为什么当前主线坚持 MiMo 基座优先，以及 SWUST 额外强化了什么 |
| [持久化记忆](/features/memory) | 想理解长任务连续性、checkpoint 和记忆如何协同 |
| [智能体模式](/features/agents) | 想理解 build / plan / compose / goal / subagent 的分工 |
| [工作流引擎](/features/workflow) | 想理解多智能体如何被脚本化和恢复执行 |

## 四条主线

<div class="swust-flow-grid">
  <a class="swust-flow-card" href="/features/agents">
    <span>01</span>
    <strong>智能体分工</strong>
    <p>用 build、plan、compose、goal 和 subagent 组织主线、调研、编排、自治和局部执行。</p>
  </a>
  <a class="swust-flow-card" href="/features/memory">
    <span>02</span>
    <strong>记忆与恢复</strong>
    <p>用 MEMORY.md、facts、checkpoint 和 task progress 保留可继续工作的上下文。</p>
  </a>
  <a class="swust-flow-card" href="/features/security">
    <span>03</span>
    <strong>工程防护</strong>
    <p>把高风险 shell、越界写入、提前停止和文档结构错误放进运行时治理。</p>
  </a>
  <a class="swust-flow-card" href="/features/workflow">
    <span>04</span>
    <strong>工作流沉淀</strong>
    <p>把重复的多智能体流程写成可恢复、可记录、可再次运行的 workflow。</p>
  </a>
</div>

## 适合的任务类型

| 场景 | 龙山灵码的处理方式 |
|------|------------------|
| 长任务修复 | 使用 goal、task 和 checkpoint 保持连续推进 |
| 多阶段实现 | 使用 compose、subagent 和 workflow 组织规划、执行、验证 |
| 项目知识积累 | 使用 memory、dream、distill 沉淀长期规则和重复工作流 |
| 工程环境操作 | 使用权限系统、Bash 安全分析和写入守卫降低误操作风险 |

## 不追求什么

龙山灵码当前不把重点放在“短平快的一问一答”或“漂亮的演示型编程体验”上。它更适合真实仓库、真实约束、真实长期任务，设计目标是让 Agent 在工程上下文里持续可用。
