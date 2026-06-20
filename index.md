---
layout: home

hero:
  name: 龙山灵码
  text: "基于 MiMo-Code 的终端原生 AI 编程智能体"
  tagline: "面向长任务的软件工程 Agent。以 MiMo-Code 为运行时基座，保留持久化记忆、checkpoint、actor 编排、goal、Compose、Dream/Distill、语音、MCP、LSP 和插件能力，并叠加 SWUST Code 的中文体验与工程防护。"
  actions:
    - theme: brand
      text: 快速开始
      link: /guide/start
    - theme: alt
      text: 主线状态
      link: /mainline-status
    - theme: alt
      text: GitHub
      link: https://github.com/MakeBlackSheepGreat/swust-code

features:
  - title: MiMo-Code 基座优先
    details: "MiMo 已有的能力保持 MiMo 原生实现，包括多 Provider、TUI、记忆、checkpoint、actor/subagent、goal、Compose、Dream/Distill、语音、MCP、LSP 和插件。"
    link: /mainline-status
  - title: 长任务上下文连续
    details: "通过持久化记忆、checkpoint、任务进度和上下文重建，让 Agent 在恢复会话或接近上下文上限时继续工作，而不是重新理解项目。"
    link: /features/memory
  - title: 多智能体工作流
    details: "build、plan、compose、goal 等主智能体配合 subagent 编排，覆盖探索、实现、评审、TDD、验证和规格驱动开发。"
    link: /features/agents
  - title: 目标驱动自治
    details: "使用 /goal 或 run --goal 设置停止条件，由独立 judge 判断目标是否真正完成，降低长任务中的过早停止风险。"
    link: /features/goal
  - title: 记忆与技能沉淀
    details: "/dream 整理长期项目知识，/distill 将重复工作流沉淀为 skill、subagent 或 command，降低后续重复劳动。"
    link: /features/dream
  - title: 工程防护
    details: "SWUST 层补充 Task Gate、Bash Safety、Write Guard、Document Validation、cache-stable 上下文和 @path 记忆导入。"
    link: /features/security
  - title: 中文优先的 TUI
    details: "侧边栏、命令面板、权限弹窗、Getting Started、路径显示、主题、attention 通知和声音包配置面向日常终端使用优化。"
    link: /features/tui
---
