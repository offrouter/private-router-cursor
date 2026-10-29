---
name: private-swap
description: Swap tokens on Robinhood Chain with OffRouter Private Swap, where the order reaches the chain only as a hash until it is filled, so there is nothing to front-run. Use when the user wants to swap, buy or sell a supported token privately.
---

# Private Swap with OffRouter

## When to use

- The user wants to swap, buy or sell a token without exposing the order to front-running.
- The user asks for a quote, or for the status of a private swap order.

## Instructions

1. Call `swap_quote` with `token_in`, `token_out`, `amount_in` (atomic units), `payer` and, if the user wants, `recipient`. ETH is `0x0000000000000000000000000000000000000000`. The tool lists what can be traded if the pair is not supported.
2. Show the quote in plain numbers: what is paid, the fee, about how much comes back and the least it will accept. Ask the user to confirm before anything is signed or sent.
3. The payer's own wallet does the next step. Never ask for, accept or handle a private key or seed phrase.
   - `method` "native" (paying in ETH): the user sends the quote's `tx` unchanged from their wallet.
   - `method` "approval": the user approves `approval.spender` for the amount once, then signs `sign` as EIP-712 typed data.
   - `method` "eip3009": the user signs `sign`. No approval and no transaction.
4. Call `swap_submit` with the quote's `intent` unchanged, plus `signature`, or `open_tx` (the transaction hash) for ETH.
5. Call `swap_status` with the order id and `order_key` (the intent's `salt`) until it reads `paid`, then give the payout transaction.
6. Tell the user to keep the salt: it is the only way to read the order. An order that is not filled is refunded to the wallet that paid.
7. Swaps are in beta, with a cap on each order. For the most privacy, suggest paying out to a fresh address.
