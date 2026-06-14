# TUI 体验

v0.3 把 TUI 从基础翻译推进到可见交互层：命令面板、权限弹窗、首页、Logo 和提示输入都接入了新的本地化与视觉逻辑。

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

TUI 现在提供 `thin` 和 `classic` 两套 SWUST Code Logo，选择会写入 `logo_design`。首页还接入了星空背景和流星动画，在普通终端模式下会自动关闭背景以避免显示问题。

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
