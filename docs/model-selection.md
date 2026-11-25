# Choosing a Kimi route

This repository documents Muapi's standard Kimi K3 endpoint. The repository slug is a discovery label: Muapi does not describe Kimi K3 as a dedicated uncensored checkpoint.

## Compare the current routes

| Route | Context | Input | Input / output per 1M tokens | Maximum output | Selection note |
|---|---:|---|---:|---:|---|
| <code>kimi-k3</code> | 1M | Text + image | $3.00 / $15.00 | 4096 | Choose when a 1M-token context window, optional image input, and Kimi K3 behavior fit the task. Confirm the live model card and pricing before production use. |

The table is a shortlist by documented interface, context, and price. It is not a quality ranking.

## A practical selection process

1. Start with input type. Use image_url only on a route whose Muapi schema lists image input.
2. Match the advertised context window to the total prompt size and leave room for the generated answer.
3. Set max_tokens to the output length your task needs; the cap varies by endpoint.
4. Estimate cost from expected input and output token counts using the separate rates.
5. For close choices, run the same prompts on each route and score them against your own criteria. This repository publishes no comparative benchmark scores.

## Model cards

- [Kimi K3](models/kimi-k3.md) — Choose when a 1M-token context window, optional image input, and Kimi K3 behavior fit the task. Confirm the live model card and pricing before production use.

Check the [Muapi live page](https://muapi.ai/playground/kimi-k3/api) for current availability and pricing.
