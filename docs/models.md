---
title: "Models"
description: "Model IDs, model-list endpoints, prices and fallback models."
canonical_url: "https://microrouter.xyz/docs/models"
markdown_url: "https://microrouter.xyz/docs/models.md"
last_updated: "2026-08-22"
---

# Models

240 language models are currently available through microrouter.
Model IDs use author/name format. Copy them exactly as returned by the API.

## Source of truth

GET https://microrouter.xyz/v1/models: OpenAI-shaped list (authenticated)
GET https://microrouter.xyz/api/v1/models: public model list with pricing,
context_length and architecture (no key required, CORS enabled).

The catalog lists text-generation models with current input and output prices.
Image, video, speech, embedding and realtime requests are not supported yet.

## Fallback models

models is an ordered list of acceptable fallback model IDs. microrouter never
uses a model outside that list.

## Unknown model

An unavailable ID returns 404 unknown_model with a did-you-mean suggestion.
