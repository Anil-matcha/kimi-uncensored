# Kimi K3 on Muapi

A hosted Kimi K3 endpoint for long-context reasoning, coding, and multimodal prompts.

| Catalog detail | Value |
|---|---|
| Muapi endpoint | <code>kimi-k3</code> |
| Context shown in Muapi catalog | 1M tokens |
| Input | Text + image |
| Input price | $3.00 per million tokens |
| Output price | $15.00 per million tokens |
| Maximum output tokens in current schema | 4096 |

## When to consider this route

Choose when a 1M-token context window, optional image input, and Kimi K3 behavior fit the task. Confirm the live model card and pricing before production use.

Context is the advertised total input window; max_tokens separately limits generated output. The live Muapi model page is the source of truth if a schema or price changes.

## Request fields

| Field | Type | Required | Notes |
|---|---|---:|---|
| <code>prompt</code> | string | Yes | Prompt text sent to the model. |
| <code>image_url</code> | string | No | Image URL; only send it to image-capable routes. |
| <code>system_prompt</code> | string | No | Optional system-level instruction. |
| <code>temperature</code> | number | No | 0–2; Kimi K3 schema default is 1. |
| <code>max_tokens</code> | integer | No | Optional output cap; route maximum is 4096. |
| <code>top_p</code> | number | No | 0–1; Kimi K3 schema default is 1. |
| <code>frequency_penalty</code> | number | No | −2–2. |
| <code>presence_penalty</code> | number | No | −2–2. |

The input object requires prompt. Other fields listed above are optional in the current schema. Include image_url only when this route lists Text + image.

## Submit and poll

Set MUAPI_KEY, submit to the endpoint, save the returned request ID, then poll the result endpoint:

```bash
curl -X POST https://api.muapi.ai/api/v1/kimi-k3 \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "Summarize the design trade-offs in this proposal.", "system_prompt": "Be concise and separate facts from assumptions.", "temperature": 0.7, "max_tokens": 1024, "top_p": 0.9}'

curl "https://api.muapi.ai/api/v1/predictions/REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_KEY"
```

The submit response contains a request_id. Poll until the job reaches a terminal status and inspect the returned result payload. Handle failed and cancelled separately from completed.

## Streaming

Muapi provides streaming on supported text-generation endpoints. Use POST /api/v1/kimi-k3/stream when the live model page confirms streaming for this route. See the [Muapi streaming guide](https://muapi.ai/docs/streaming) and this repository's [streaming example](../../examples/stream.py).

## Pricing

Muapi's catalog currently lists $3.00/M input tokens and $15.00/M output tokens. Actual charge depends on request usage. Verify the live [Muapi catalog](https://muapi.ai/playground/kimi-k3) before budgeting.

## Links

- [Muapi model page](https://muapi.ai/playground/kimi-k3)
- [Muapi API reference](https://muapi.ai/docs/api-reference)
- [Family selection guide](../model-selection.md)
