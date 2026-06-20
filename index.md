---
layout: home

hero:
  name: 龙山灵码
  text: 终端原生 AI 编程智能体
  tagline: 基于 MiMo-Code 构建，继承持久化记忆、checkpoint、actor 编排、goal、Compose、Dream/Distill 和语音能力，并保留 SWUST Code 的工程化增强。
  actions:
    - theme: brand
      text: 快速开始
      link: /guide/start
    - theme: alt
      text: GitHub
      link: https://github.com/MakeBlackSheepGreat/swust-code

features:
  - icon: 🧠
    title: 持久化记忆
    details: SQLite FTS5 索引、MEMORY.md 注入、@path 导入、checkpoint writer 和 one-fact-per-file 项目知识存储。
    link: /features/memory
  - icon: 🧭
    title: 智能体模式
    details: build、plan、compose、goal、explore 多智能体，subagent 编排和 checkpoint-writer 均为 MiMo-Code 原生实现。
    link: /features/agents
  - icon: 🎯
    title: 目标驱动自治
    details: /goal 命令设置停止条件，独立 LLM Judge 评估目标是否达成，防止过早停止。
    link: /features/goal
  - icon: 🌱
    title: 自我进化
    details: /dream 扫描会话轨迹提取持久知识，/distill 发现重复工作流并打包为可复用技能。
    link: /features/dream
  - icon: 🛡️
    title: 安全防护
    details: 四步权限流水线 + Bash 命令安全分析，fail-closed 默认策略。
    link: /features/security
  - icon: ⚙️
    title: 工作流引擎
    details: JavaScript 工作流可执行 host 函数、派生子 Agent，并写入持久化 JSONL journal。
    link: /features/workflow
  - icon: 🧩
    title: 技能系统
    details: SKILL.md 声明式技能，compose hidden skills 和动态 catalog 已接入运行时。
    link: /features/skills
  - icon: 🌐
    title: 中英文 TUI
    details: 命令面板、权限弹窗、语言切换、Logo 选择和下一条输入预测已接入 TUI。
    link: /features/i18n
  - icon: ✦
    title: TUI 体验
    details: 星空首页、双 Logo、龙山灵码主题和 ghost suggestion 改善日常终端交互。
    link: /features/tui
---
