---
name: private-inference
description: Ask a private model on OffRouter, or compare several, served in a GPU enclave with nothing logged and a signed receipt. Use for a second opinion on sensitive code, contracts, strategies or anything that should not be kept by a model provider.
---

# Private inference with OffRouter

## When to use

- The user wants a second opinion on code, a smart contract or a plan from a model that does not log it.
- The user asks for a specific open model (DeepSeek, Qwen, GLM, Kimi, Gemma, gpt-oss and others).
- The user wants to compare how several models answer the same question.

## Instructions

1. Call `list_models` if you need to pick a model. Prefer one whose context length fits the input.
2. Build the prompt. Include only the code and context the question needs, and redact secrets such as private keys, seed phrases and API keys.
3. Call `ask` with the model and prompt, or `compare` with two to four models for the same prompt.
4. Give the user the answer, then one line with the model, the cost and the receipt link from the result.
5. Without a key, `ask` is answered by the free demo model, a few calls a day, and `compare` and `balance` need a key. If the user wants more, point them to the plugin's README to add `OFFROUTER_API_KEY`.
6. `balance` shows what is left on the key and the recent spend.
