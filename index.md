---
layout: home

hero:
  name: SWUST Code
  text: 终端原生 AI 编程智能体
  tagline: 基于 OpenCode v1.17.4 构建，整合 MiMo-Code、DevEco Code 与 DeepSeek-Reasonix 的记忆、自治、工具和缓存能力。
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
    details: SQLite FTS5 索引、MEMORY.md 注入、@path 导入和 one-fact-per-file 项目知识存储。
    link: /features/memory
  - icon: 🎯
    title: 目标驱动自治
    details: Goal/Gate 已接入独立 LLM Judge，未达成时自动发布提醒并继续工作。
    link: /features/goal
  - icon: 🌱
    title: 自我进化
    details: Dream 和 Distill 会启动带目标的自治 run，并支持 7/30 天后台自动触发。
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
    details: SKILL.md 声明式技能，支持项目、全局和外部目录发现。
    link: /features/skills
  - icon: 🌐
    title: 中英文 TUI
    details: 命令面板、权限弹窗、语言切换、Logo 选择和下一条输入预测已接入 TUI。
    link: /features/i18n
  - icon: ✦
    title: TUI 体验
    details: 星空首页、双 Logo、SWUST Code 主题和 ghost suggestion 改善日常终端交互。
    link: /features/tui
---
