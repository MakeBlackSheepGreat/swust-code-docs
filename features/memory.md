# 持久化记忆

SWUST Code 的记忆系统让你的 AI 编程助手跨会话记住项目知识。

## 工作原理

记忆以 Markdown 文件为源数据，并同步到 SQLite FTS5 全文搜索索引。核心 v2 runner 会在构建 system context 时加载记忆上下文，将全局 `MEMORY.md` 内容注入 system prompt（4KB 上限）。长会话接近上下文上限时，v0.4 会优先启动 checkpoint writer 写入会话检查点，再通过 checkpoint boundary 重建上下文。

## 记忆目录结构

```
~/.local/share/swust-code/memory/
  global/
    MEMORY.md              # 跨项目用户偏好
  projects/
    <project_hash>/
      MEMORY.md            # 项目知识
      facts/
        <fact>.md          # one-fact-per-file 事实存储
      architecture.md      # 架构决策
      rules.md             # 项目规则
  sessions/
    <session_id>/
      checkpoint.md        # 会话检查点（11 段结构）
      notes.md             # 临时笔记
      tasks/
        <task_id>/
          progress.md      # 子 Agent 任务进度
```

## 记忆工具

### memory（搜索）

核心 v2 工具注册表包含 `memory` 工具，可搜索记忆：

```json
{
  "query": "认证模块 JWT 配置",
  "kind": "project",
  "limit": 5
}
```

使用 BM25 排序，1-3 个关键词效果最佳。

### memory_write（写入）

核心 v2 工具注册表包含 `memory_write` 工具，可写入记忆：

```json
{
  "scope": "projects",
  "scopeId": "abc123",
  "key": "MEMORY.md",
  "content": "## 架构决策\n使用 JWT 进行用户认证...",
  "mode": "append"
}
```

## 自动行为

- **搜索前同步**：每次搜索前自动将磁盘文件同步到 FTS 索引
- **上下文注入**：会话启动时自动注入 MEMORY.md 内容（4KB 上限）
- **增量同步**：基于文件大小和修改时间的指纹比对，只处理变化文件
- **导入展开**：`MEMORY.md` 支持 `@path` 导入，本地解析时会展开引用内容
- **Checkpoint writer**：上下文溢出前启动后台系统 Agent，写入 `checkpoint.md`、`MEMORY.md` 和任务进度摘要
- **Boundary rebuild**：writer 完成后记录 `last_checkpoint_message_id`，后续只保留 checkpoint 后的必要 tail

## 技术细节

- **存储**：SQLite FTS5 虚拟表 + 外部内容模式
- **分词**：Unicode regex `/[\p{L}\p{N}_]+/u`，支持中日韩
- **排序**：BM25 + 相对分数阈值（top_hit × 0.15）
- **同步**：Semaphore(1) 并发控制，懒触发
- **路径范围**：`global`、`projects/<project_id>`、`sessions/<session_id>`
- **Writer 队列**：同一 session 只运行一个 checkpoint writer，新请求覆盖 pending 范围
