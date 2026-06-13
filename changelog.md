# 更新日志

## v0.2.0 (2026-06-14)

移植自 DeepSeek-Reasonix（esengine）和 MiMo-Code/Claude-Code 的 Session 增强。

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

- 17 种语言类型定义，支持 en/zh/zht/ja/ko/de/es/fr/ru 等
- 三层语言自动检测：时区 → 环境变量 → Intl API
- SolidJS 响应式语言上下文，懒加载 + 缓存
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
- Goal Judge 独立评估
- Task Gate 二级停止条件
- 重入控制（主 12 次 / 子 3 次）

**自我进化**
- Dream 知识提炼（7 天周期）
- Distill 技能发现（30 天周期）
- 自动触发机制

**安全防护**
- 四步权限流水线
- Bash 命令安全分析器
- fail-closed 默认策略

**多 Agent 编排**
- Actor/Spawn 子 Agent 系统
- Fork Cache 对齐
- Coordinator 协议

**工作流引擎**
- QuickJS 沙箱运行时
- Journal 持久化 + 崩溃恢复
- Deep Research 内置工作流

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
