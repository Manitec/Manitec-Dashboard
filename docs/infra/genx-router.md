# GenX Router API

**What it is:** DashNex's unified AI API — one key, 40+ models. Text, image, video, and audio generation from a single endpoint.

**Site:** [genx.sh](https://genx.sh)

**Base URL:** `https://query.genx.sh/api/v1`

## Key Features

- Single API key replaces ALL provider accounts
- 40+ models: GPT, Claude, Gemini, Grok, Sora, Veo, Kling, and more
- Async job system — submit → get `job_id` → poll or use webhook
- Stateful sessions with multi-turn chat, tool use, auto-compaction
- File uploads up to 100MB (PDF, DOCX, CSV, etc.)
- **500 free credits on signup**
- Credits never expire, shared across entire DashNex ecosystem

## Billing Tiers

| Tier | Discount | Rate Limit | Concurrency |
|---|---|---|---|
| Starter | — | 10 RPM | 2 |
| Blaze | 5% off | 60 RPM | 5 |
| Agent | 10% off | 200 RPM | 10 |
| Operator | 15% off | 500 RPM | 25 |

## Quick Start

```bash
curl -X POST https://query.genx.sh/api/v1/generate \
  -H "Authorization: Bearer gnxk_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "claude-sonnet-4-6", "params": {"prompt": "Hello world"}}'
```

## Relevance to Manitec

Could replace Groq in ManiBot — giving access to Claude, Gemini, image/video generation all from one key already available through DashNex.
