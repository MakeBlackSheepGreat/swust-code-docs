# 更新日志

## v0.1.0 (2026-06-13)

### 初始版本

基于 OpenCode v1.17.4 构建，移植自 MiMo-Code、DevEco Code 和 DeepSeek-Reasonix。

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

**缓存优先架构（移植自 DeepSeek-Reasonix）**
- System prompt 分为字节稳定前缀 + 每轮 tail
- 前缀在会话内保持不变，LLM Provider 缓存持续命中

**记忆增强（移植自 DeepSeek-Reasonix）**
- `@path` 导入指令：MEMORY.md 中可导入其他文件
- One-Fact-Per-File 存储：每个事实一个 md 文件 + frontmatter
- Slash 命令：`/memory` `/goal` `/dream` `/distill` 交互式命令

**Session 增强（移植自 MiMo-Code + Claude-Code）**
- Retry 策略：header-aware 指数退避，transient error 检测
- Doom Loop 检测：3 次相同 tool call 自动打断
- Token 估算：三层估算 + auto-compact 阈值
- Tool Output 裁剪：保护最近 40K tokens，旧 tool output 标记为 compacted

### 统计

- 62+ 个新源文件
- 11 个测试文件（154 个测试用例，全部通过）
- 24 个 CLI 命令
- 15+ LLM 提供商支持
- 4 个参考项目：OpenCode、MiMo-Code、DevEco Code、DeepSeek-Reasonix
