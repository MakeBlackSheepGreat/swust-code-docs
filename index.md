---
layout: home

hero:
  name: 龙山灵码
  text: "基于 MiMo-Code 的终端原生 AI 编程智能体"
  tagline: "面向长任务的软件工程 Agent。龙山灵码继承 MiMo-Code 的记忆、checkpoint、子智能体编排、goal、Compose、Dream/Distill、MCP、LSP 和插件能力，再叠加中文优先的终端体验、工程防护和项目级治理能力。"
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
    details: "持久化记忆、checkpoint、任务进度和上下文重建共同工作，让会话恢复、上下文溢出和长链路任务都能继续推进，而不是重新理解项目。"
    link: /features/memory
  - title: 多智能体协作
    details: "build、plan、compose、goal 与 subagent 构成统一运行时，可覆盖规划、并行执行、评审、验证和目标驱动自治。"
    link: /features/agents
  - title: 工程防护
    details: "在 MiMo 基座之上，SWUST 额外加强了 Task Gate、Bash Safety、Write Guard、Document Validation 和上下文治理，适合真实工程环境。"
    link: /features/security
  - title: 中文优先 TUI
    details: "侧边栏信息组织、命令区别名、提示反馈、主题与阅读节奏面向中文开发者优化，而不是仅做品牌替换。"
    link: /features/tui
  - title: 可演进的项目知识
    details: "通过 /dream 和 /distill，把长期项目知识和重复工作流持续沉淀为记忆、技能、子智能体或命令。"
    link: /features/dream
  - title: 子智能体个性化
    details: "可见子智能体支持项目级模型、思考强度和最大步数设置，便于把不同角色智能体约束到具体工程策略里。"
    link: /features/agents
---

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

## 适合的任务类型

| 场景 | 龙山灵码的处理方式 |
|------|------------------|
| 长任务修复 | 使用 goal、task 和 checkpoint 保持连续推进 |
| 多阶段实现 | 使用 compose、subagent 和 workflow 组织规划、执行、验证 |
| 项目知识积累 | 使用 memory、dream、distill 沉淀长期规则和重复工作流 |
| 工程环境操作 | 使用权限系统、Bash 安全分析和写入守卫降低误操作风险 |

## 不追求什么

龙山灵码当前不把重点放在“短平快的一问一答”或“漂亮的演示型编程体验”上。它更适合真实仓库、真实约束、真实长期任务，设计目标是让 Agent 在工程上下文里持续可用。
