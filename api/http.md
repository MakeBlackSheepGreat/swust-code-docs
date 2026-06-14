# HTTP API

`swust-code serve` 和 `swust-code web` 暴露实验性 HTTP API。v0.3 的 OpenAPI 标题和 SDK 注释已统一为 SWUST Code，并新增会话预测接口。

## 会话预测

```http
POST /session/{sessionID}/predict
```

用途：为 TUI 空输入框生成下一条消息预测，也可供外部客户端做轻量提示补全。

| 参数 | 位置 | 说明 |
|------|------|------|
| `sessionID` | path | 会话 ID |
| `directory` | query | 可选，指定运行目录 |
| `workspace` | query | 可选，指定 workspace |

响应：

```json
{
  "prediction": "继续修复剩下的类型错误"
}
```

服务端会读取最近一次真实用户消息和后续完成的 assistant 回复，使用 small/title 模型生成不超过约 120 字符的短句。配置 `experimental.predict_next_prompt=false` 时返回空字符串。

## SDK

生成的 JS SDK 已包含：

```typescript
sdk.client.session.predict({
  sessionID,
  directory,
  workspace,
})
```

预测失败会在 TUI 侧静默降级为空建议。
