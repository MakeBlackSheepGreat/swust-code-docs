# HTTP API

`swust-code serve` and `swust-code web` expose the experimental HTTP API. v0.3 aligns OpenAPI titles and SDK comments with SWUST Code branding and adds a session prediction endpoint.

## Session Prediction

```http
POST /session/{sessionID}/predict
```

Use this to generate a likely next prompt for an idle TUI input box, or as lightweight prompt completion for external clients.

| Parameter | Location | Description |
|-----------|----------|-------------|
| `sessionID` | path | Session ID |
| `directory` | query | Optional working directory |
| `workspace` | query | Optional workspace |

Response:

```json
{
  "prediction": "continue fixing the remaining type errors"
}
```

The server reads the latest real user message and the completed assistant responses after it, then uses a small/title model to produce a short suggestion. If `experimental.predict_next_prompt=false`, the endpoint returns an empty string.

## SDK

The generated JS SDK includes:

```typescript
sdk.client.session.predict({
  sessionID,
  directory,
  workspace,
})
```

The TUI silently falls back to an empty suggestion if prediction fails.
