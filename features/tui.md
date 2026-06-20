# TUI 体验

龙山灵码的 TUI 基于 MiMo-Code 运行时扩展，并保留旧 SWUST Code 的侧边栏体验。除命令面板、权限弹窗、首页、Logo 和提示输入外，侧边栏会展示工作目录、指令文件、getting-started 提示、Goal、Task、Todo、LSP/MCP、变更文件、上下文窗口、token、费用和缓存指标。

## 侧边栏

侧边栏默认服务于长会话和自治任务的运行态观察：

- 工作目录和指令文件位置
- Goal、Task、Todo 当前状态
- LSP、MCP、变更文件
- 上下文窗口健康度、请求 token、会话 token、压缩触发状态
- 本轮费用、会话费用、cache read/write 和 cache hit
- 免费模型与 Provider 配置的 getting-started 提示

`TuiPathsProvider` 已接入 app runtime，插件和侧边栏组件可以稳定读取当前工作目录、配置路径和运行时路径。

## Attention 通知

新 TUI 已接入 attention 通知与声音包配置。相关配置位于 `tui.json` / `tui.jsonc` 的 `attention` 字段，可控制是否启用通知、声音、音量和 sound pack。

## 命令面板

命令名和 slash 入口保持稳定，例如 `/models`、`/language`、`/logo`；描述和分类会按当前语言显示。这样快捷命令不会随语言变化，中文用户仍能看到本地化说明。

## 语言切换

```text
/language
```

语言偏好写入 TUI KV：

- `auto`：跟随系统检测
- `en`：英文
- `zh`：简体中文
- 其他 locale 目前保留标签和类型，字典仍需补齐

`SWUST_CODE_LOCALE` 环境变量优先级更高，可用于固定启动语言。

## Logo 与首页

```text
/logo
```

TUI 现在提供 `thin` 和 `classic` 两套龙山灵码 Logo，选择会写入 `logo_design`。首页还接入了星空背景和流星动画，在普通终端模式下会自动关闭背景以避免显示问题。

主题默认注册了 `swust-code` 主题名，深色主题色调整为蓝色系主色、青色辅助和紫色强调。

## 下一条输入预测

会话空闲后，TUI 会调用 `POST /session/{sessionID}/predict` 生成下一条输入建议：

- 空输入框时显示 ghost suggestion
- `Tab` 采纳
- `Esc` 关闭
- 用户开始输入、会话状态变化或切换会话时自动清空

可以在配置里关闭：

```json
{
  "experimental": {
    "predict_next_prompt": false
  }
}
```
