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
    details: 设定目标后 Agent 进入 Goal/Gate 重入循环；独立 Judge 模型接入仍在完善。
    link: /features/goal
  - icon: 🌱
    title: 自我进化
    details: Dream 和 Distill 命令已接入 CLI；自动周期调度仍在接入会话生命周期。
    link: /features/dream
  - icon: 🛡️
    title: 安全防护
    details: 四步权限流水线 + Bash 命令安全分析，fail-closed 默认策略。
    link: /features/security
  - icon: ⚙️
    title: 工作流引擎
    details: JavaScript 编排运行时骨架已存在，脚本执行、沙箱和持久化恢复仍在接入。
    link: /features/workflow
  - icon: 🧩
    title: 技能系统
    details: SKILL.md 声明式技能，支持项目、全局和外部目录发现。
    link: /features/skills
  - icon: 🌐
    title: 中英文 TUI
    details: TUI 命令面板、提示和常用控件已接入中文/英文翻译，默认跟随系统语言。
    link: /features/i18n
---
