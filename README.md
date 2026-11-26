 # LLM Request Cost Calculator

A small educational project: how the context window works and what a chat with an LLM really costs.

## The Problem

An LLM has no memory between requests. Every call resends the full history: system prompt, all previous messages and tool outputs. This means:

- the longer the chat, the more tokens you pay for on every turn;
- output tokens cost 4–6x more than input tokens;
- a "cheap" model is not always a cheap chat.

## Formula

cost = (input_tokens / 1000) * price_in + (output_tokens / 1000) * price_out

## What's Inside

- `cost function` — one-request cost calculation;
- `100 identical requests` — mass-processing scenario;
- `10-turn chat` — simulation where the full history is resent each turn;
- `plots` — cost growth per turn and input/output split.

## Results

Prices per 1M tokens (November 2026, USD):

| Model | Input | Output | 100 requests | 10-turn chat |
|---|---|---|---|---|
| Gemini 2.0 Flash | $0.10 | $0.40 | $0.017 | $0.00375 |
| GPT-4o mini | $0.15 | $0.60 | $0.026 | $0.0056 |
| GPT-5.4 Nano | $0.20 | $1.25 | $0.048 | $0.0089 |
| Claude Haiku 4.5 | $1.00 | $5.00 | $0.20 | $0.0405 |

Key numbers:

- on turn 10, **94% of the request** is resent history;
- a 10-turn chat costs **~2.2x more** than 10 independent requests;
- the gap between the cheapest and priciest model is **~11x** on the same task.

## Takeaways

1. In a chat you mostly pay for memory, not for answers.
2. Model choice is an economics decision, not just a quality one.
3. Mitigations: summarize the history, use prompt caching.

Prices change often — check the provider's pricing page before using in production.
