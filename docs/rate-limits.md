---
title: "Rate limits"
description: "Per-key request, token and spend limits plus size constraints."
canonical_url: "https://microrouter.xyz/docs/rate-limits"
markdown_url: "https://microrouter.xyz/docs/rate-limits.md"
last_updated: "2026-08-22"
---

# Rate limits

Limits are per key and enforced at the edge:

- rpmLimit: requests per minute
- tpmLimit: estimated input and output tokens per minute
- dailyLimitNano: daily spend cap in nano-USD
- monthlyLimitNano: monthly spend cap in nano-USD

Defaults are lower for accountless keys. Raise any limit per key in the
dashboard. Open reservations count immediately, so concurrent requests cannot
bypass token or spend caps.

## The 429 response

Every 429 carries Retry-After and names the limit that was reached and where to
raise it: https://microrouter.xyz/docs/errors#rate_limited

## Body and context size

Request bodies over 10 MB are refused with 413 before being read fully:
https://microrouter.xyz/docs/errors#payload_too_large

Context that exceeds a model's window returns 400:
https://microrouter.xyz/docs/errors#context_too_long
