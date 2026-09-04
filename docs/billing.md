---
title: "Billing"
description: "Credit pricing, deposits, refunds, chargebacks and low-balance behavior."
canonical_url: "https://microrouter.xyz/docs/billing"
markdown_url: "https://microrouter.xyz/docs/billing.md"
last_updated: "2026-08-22"
---

# Billing

Units are pegged: 1,000 credits = $1. Checkout shows only payment methods
reported available by the backend for that account; an unavailable provider is
not presented as live. Charges are metered in nano-USD, and every response
reports its exact cost in usage.cost and the x-microrouter-cost-usd header.

## Deposits only

- Direct Robinhood Chain minimum $0.50. Relay and other crypto providers start at $5.
- There are no withdrawals. Credits buy inference and are not a withdrawable balance.
- Lose an accountless key and the balance goes with it. This is stated before payment.
- Credits never expire.

## Refunds

Service credit only, never cash. Policy:
https://microrouter.xyz/legal/refunds

## Chargebacks (cards, when configured)

Unconfigured card checkout is not shown as available. Card-funded credit is
tracked separately. A chargeback posts a reversing ledger
transaction, taking the balance negative if the credit has already been spent,
and suspends the account pending resolution:
https://microrouter.xyz/docs/errors#account_suspended

## Running low

- A pre-request 402 is returned once the balance is below the estimated cost:
  https://microrouter.xyz/docs/errors#insufficient_credits
- x-microrouter-balance-usd is included on every response.
- Where possible, max_tokens is clamped to what the balance affords and the
  response carries x-microrouter-max-tokens-clamped: true.
