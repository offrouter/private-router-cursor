# OffRouter Private Router for Cursor

The private router for onchain agents, in Cursor. [OffRouter](https://offrouter.org) runs open models (DeepSeek, Qwen, GLM, Kimi, Gemma, gpt-oss and more) inside GPU enclaves, Intel TDX with an NVIDIA confidential GPU. Nothing is logged, and every answer comes back with a signed receipt you can check. Private Swap trades tokens on Robinhood Chain with the order sealed: the chain sees only a hash until it is filled, so there is nothing to front-run.

This plugin connects Cursor to OffRouter's MCP server at `https://offrouter.org/mcp`. There is nothing to install and nothing runs on your machine.

## What's inside

| | |
| --- | --- |
| MCP server `offrouter` | the hosted OffRouter MCP server |
| Skill `private-inference` | ask one private model, or compare two to four, and report cost and receipt |
| Skill `private-swap` | quote, submit and follow a sealed token swap, signed by your own wallet |
| Rule `offrouter` | when to reach for OffRouter, and never to paste secrets or hand over a private key |

Tools: `list_models`, `ask`, `compare`, `balance`, `swap_quote`, `swap_submit` and `swap_status`.

## Install

Install **OffRouter Private Router** from the Cursor Marketplace, or try it from this repository:

```bash
git clone https://github.com/offrouter/private-router-cursor ~/.cursor/plugins/local/offrouter-private-router
```

Then run **Developer: Reload Window**.

## Try it, then add a key

With nothing configured, `ask` is answered by OffRouter's free demo: one model and a few calls a day. `list_models` and the swap tools need no key at all. Ask the agent something like "ask a private model on OffRouter to review this function".

For every model, `compare` and `balance`, create a prepaid key (`off_sk_…`) at [offrouter.org/dashboard](https://offrouter.org/dashboard) and set it in your environment before starting Cursor:

```bash
export OFFROUTER_API_KEY=off_sk_...
```

The plugin sends it as `Authorization: Bearer $OFFROUTER_API_KEY`. Each call is charged the exact token cost.

## What stays private

- The model runs in a GPU enclave that its own host cannot read. Prompts and answers are never stored or logged, and each answer has a receipt signed inside the enclave.
- OffRouter's gateway handles the request in memory while forwarding it to the enclave. To keep even the gateway out of the path, run the open-source [OffRouter MCP server](https://github.com/offrouter/mcp) locally instead: it encrypts each prompt on your machine to a key the enclave proves it holds.
- Swaps: what you buy, your minimum and your recipient stay in an enclave until the order is filled. Your payment into escrow and the payout are on chain.
- Cursor itself sees your prompts and the answers, since that is where they come from and go to.

## Links

- [offrouter.org](https://offrouter.org) · [Docs](https://docs.offrouter.org) · [Models](https://offrouter.org/models) · [Private Swap](https://offrouter.org/swap)
- [OffRouter MCP server, local](https://github.com/offrouter/mcp)
- [@OffRouter on X](https://x.com/OffRouter)

## License

MIT
