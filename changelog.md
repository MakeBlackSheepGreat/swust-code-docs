# 更新日志

## v0.3.0 (2026-06-14)

根据当前 `swust-code` 最新代码状态更新文档站：本版重点是把 0.2 中仍处于占位或待接入的能力推进到可运行路径，并补齐 TUI 体验文档。

### 目标驱动自治

- Goal Judge 已接入 `LLM.generateObject()`，按 `Verdict` schema 输出 `ok`、`impossible`、`reason`
- core runner 会组装会话转录、工具结果、shell 输出和压缩摘要供 Judge 评估
- 目标未达成时发布 synthetic reminder 并继续，Judge 调用失败时按未达成处理
- Task Gate 的真实 `todowrite` 状态接入仍待后续完善

### Dream / Distill 自我进化

- `swust-code dream` 和 `swust-code distill` 改为启动带 `--goal` 的自治 run
- 新增通用自治任务 runner，支持 `--dry-run`、`--yes`、`--model`、`--agent`、`--dir`
- 会话结束后按 7 天 Dream、30 天 Distill 检查后台自动触发
- 新增 `SWUST_CODE_AUTO_EVOLUTION=0|false` 禁用开关，子进程自动设置为 `0` 防止递归触发

### 工作流引擎

- 工作流 runtime 已执行脚本，注入 `agent`、`parallel`、`pipeline`、`phase`、`log`、`workflow` 和 `args`
- `agent()` 通过 Actor Spawn 派生 ephemeral subagent，并记录运行计数
- 新增持久化 JSONL journal、脚本保存、脚本变更失效检测和结果重放
- 内置 `deep-research` 工作流可通过注册表调用

### TUI 体验

- 新增 `/language` 语言切换对话框，偏好写入 TUI KV
- 命令面板、权限弹窗、提示输入、侧边栏和常用对话框接入中英文翻译
- 新增 `/logo` Logo 设计切换，提供 `thin` 与 `classic` 两套 SWUST Code Logo
- 首页新增星空背景和流星动画，普通终端模式下自动关闭
- 新增下一条输入预测：`POST /session/{sessionID}/predict`、TUI ghost suggestion、`Tab` 采纳、`Esc` 关闭
- 新增 `experimental.predict_next_prompt=false` 配置开关

### 品牌化与安全

- 系统提示词、OpenAPI 标题、SDK 注释、终端标题和文档链接统一为 SWUST Code
- 默认主题名和 `swust-code` 主题注册修正
- `.gitignore` 增补 auth、credential、env 相关敏感文件，提供 `.env.example`

---

## v0.2.0 (2026-06-14)

移植自 DeepSeek-Reasonix（esengine）和 MiMo-Code/Claude-Code 的 Session 增强。

### 文档状态校准

- 根据当前 `swust-code` 代码重新校准文档站描述
- 修正 Goal Judge、Dream/Distill 自动调度、Workflow QuickJS、技能条件激活和 i18n 的成熟度说明
- 新增英文 API 参考与配置 Schema 页面

### 缓存优先架构（移植自 DeepSeek-Reasonix）

- System prompt 分为字节稳定前缀 + 每轮 tail
- 前缀在会话内保持不变，LLM Provider 缓存持续命中
- 降低长会话的 token 成本

### 记忆增强（移植自 DeepSeek-Reasonix）

- `@path` 导入指令：MEMORY.md 中可 `@path` 导入其他文件，递归解析，深度限制 5
- One-Fact-Per-File 存储：每个事实一个 md 文件 + frontmatter，MEMORY.md 自动索引
- Slash 命令：`/memory` `/goal` `/dream` `/distill` `/help` 交互式命令

### Session 增强

- **Retry 策略**（移植自 MiMo-Code）：header-aware 指数退避，transient error 检测（429/5xx/ECONNRESET）
- **Doom Loop 检测**（移植自 MiMo-Code）：3 次相同 tool call + 相同 input 自动打断循环
- **Token 估算**（移植自 Claude-Code）：三层估算（rough → API → fallback），auto-compact 阈值，context window 管理
- **Tool Output 裁剪**（移植自 DevEco Code）：保护最近 40K tokens，旧 tool output 标记为 compacted

### 国际化（移植自 MiMo-Code）

- 17 种语言类型定义，当前完整字典落地为 en/zh，其余 locale 保留类型与标签
- 三层语言自动检测：时区 → 环境变量 → Intl API
- SolidJS 响应式语言上下文，TUI 可视化切换入口仍在接入
- 中文翻译字典（50+ keys），覆盖 prompt/tips/dialog/toast
- CLI 级别同步翻译函数
- CJK 字符宽度自动处理（Bun.stringWidth）

### 代码质量

- 接入所有孤立模块（import-resolver、token-estimation、fact-store）
- 消除重复代码，统一使用共享工具函数
- 全面审计：10 个模块接入状态验证，6 个孤立模块修复

### 凭证导入

- `swust-code providers import` 一键导入 API Key
- 支持从 MiMo-Code、Claude Code、环境变量导入
- 非破坏性：已有凭证不会被覆盖

### 统计

- 新增 14 个源文件
- 累计 70+ 个新源文件，154 个测试用例

---

## v0.1.0 (2026-06-13)

### 初始版本

基于 OpenCode v1.17.4 构建，移植自 MiMo-Code（小米）和 DevEco Code（nicognaW）。

### 核心特性

**持久化记忆系统**
- FTS5 全文搜索 + BM25 排序
- 增量同步引擎（size-mtime 指纹）
- `memory` 搜索工具 + `memory_write` 写入工具
- MEMORY.md 自动注入 system prompt
- 三级作用域：global / project / session

**目标驱动自治**
- `--goal` CLI 参数
- Goal Store、Goal Gate 和重入控制已接入
- 当前 runner 的 Judge 评估仍是占位实现
- Task Gate 状态与 todowrite 的完整联动仍在后续接入
- 重入控制（主 12 次 / 子 3 次）

**自我进化**
- Dream 知识提炼 CLI 与专用提示词
- Distill 技能发现 CLI 与专用提示词
- 周期判断代码存在，自动调度函数当前返回 false

**安全防护**
- 四步权限流水线
- Bash 命令安全分析器
- fail-closed 默认策略

**多 Agent 编排**
- Actor/Spawn 子 Agent 系统
- Fork Cache 对齐
- Coordinator 协议

**工作流引擎**
- Workflow runtime 骨架、metadata 解析和内存 journal
- QuickJS 沙箱、host 函数注入和持久化恢复仍在后续增强
- Deep Research 相关文件已存在，完整执行链路仍需继续接入

**扩展性**
- 动态工具加载（JSON 声明式）
- NAPI 原生工具桥接
- Workspace 适配器
- 文档验证系统

### 统计

- 53 个新源文件（6,380 行新代码）
- 99 个测试用例（全部通过）
- 24 个 CLI 命令
- 15+ LLM 提供商支持
