# Kimi K3 API with Muapi

Call Moonshot Kimi K3 through Muapi's REST API. This guide covers the async endpoint, live SSE streaming, supported request fields, and runnable Python and cURL examples.

The repository name uses the requested search phrase. It documents Muapi's standard Kimi K3 endpoint; Muapi does not currently label this route as a separately modified uncensored checkpoint, and no no-refusal behavior is promised.

## Related Projects

- [Muapi Uncensored AI API guide](https://github.com/Anil-matcha/Uncensored-AI-API) — API setup and model-specific examples for Muapi's abliterated LLM endpoints.
- [Awesome Abliterated LLMs](https://github.com/Anil-matcha/awesome-abliterated-llms) — broader model comparison and evaluation guide.
- [Open Generative AI](https://github.com/Anil-matcha/Open-Generative-AI) — a creative AI workspace that connects to Muapi.

## Muapi model

Muapi exposes Kimi K3 as a hosted text-generation model with a 1M-token context window and optional image input. The current Muapi catalog lists token pricing of **$3 per million input tokens** and **$15 per million output tokens**. Check the [Kimi K3 playground](https://muapi.ai/playground/kimi-k3) for current availability and pricing before production use.

| Item | Value |
|---|---|
| Async endpoint | **POST https://api.muapi.ai/api/v1/kimi-k3** |
| Streaming endpoint | **POST https://api.muapi.ai/api/v1/kimi-k3/stream** |
| Input | Required **prompt**; optional **image_url**, **system_prompt**, **temperature**, **max_tokens**, **top_p**, **frequency_penalty**, **presence_penalty** |
| Output limit | **max_tokens** from 1 to 4,096 |
| Context window | Up to 1M tokens |
| Authentication | **x-api-key** header |

The 1M-token context window is an upstream model limit, not a promise that every request at that length will fit a particular account, request, or service configuration. The model's response behavior is not guaranteed; evaluate it for your use case and follow Muapi's terms.

## Quick start

Create a key in [Muapi API Keys](https://muapi.ai/access-keys), then set it in your shell:

~~~bash
export MUAPI_KEY="your-muapi-key"
~~~

Submit a prompt:

~~~bash
curl -X POST https://api.muapi.ai/api/v1/kimi-k3 \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Explain mixture-of-experts models in three concise paragraphs.",
    "max_tokens": 1200,
    "temperature": 0.7
  }'
~~~

The submit response includes a **request_id**. Poll for the result:

~~~bash
curl "https://api.muapi.ai/api/v1/predictions/REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_KEY"
~~~

For live token delivery, use SSE:

~~~bash
curl -N https://api.muapi.ai/api/v1/kimi-k3/stream \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt":"Give me three practical ways to summarize a long technical document."}'
~~~

## Python example

Requires Python 3.9+ and **requests**. This example submits a job, polls until it finishes, and prints Muapi's full result JSON.

~~~bash
python -m pip install -r requirements.txt
python examples/submit.py "Explain how to design a reliable job queue."
~~~

## Links

- [Kimi K3 on Muapi](https://muapi.ai/playground/kimi-k3)
- [Muapi API reference](https://muapi.ai/docs/api-reference)
- [Create or manage an API key](https://muapi.ai/access-keys)
- [Muapi](https://muapi.ai)

Prices and model availability can change. This guide describes the Muapi catalog checked on 2026-11-25; the live Muapi page is authoritative.
