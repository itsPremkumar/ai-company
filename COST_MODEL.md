# Cost Model — Running the AI-Operated Company

> Monthly cost estimates for self-hosting the full stack.
> All prices in USD. Updated July 2026.

## Server Costs (Hetzner / OVH / Netcup)

| Tier | Spec | Provider | Monthly | Runs |
|---|---|---|---|---|
| **MVP** | 4 vCPU / 16 GB / 200 GB | Hetzner CX52 | ~$35 | Core DBs + n8n + Chatwoot + Open WebUI + Mautic |
| **Growth** | 8 vCPU / 32 GB / 500 GB | Hetzner CCX23 | ~$75 | Full core 20 + Grafana + Loki + Meilisearch + Airbyte |
| **Scale** | 16 vCPU / 64 GB / 1 TB | Hetzner CCX33 | ~$150 | Everything + staging + redundancy + GPU inference |
| **GPU node** | 1× RTX 4090 / 16 vCPU / 64 GB | Hetzner GEX44 | ~$250 | Ollama + local LLM inference (7B–70B models) |

**Storage add-ons:**
- MinIO on separate volume: ~$10/mo for 500 GB (Hetzner Volume)
- S3-compatible backup (Backblaze B2): ~$5/mo per TB
- PostgreSQL backups: ~$3/mo per 100 GB

## LLM API Token Costs

### Recommended Model per Department

| Department | Recommended Model | Provider | Input / 1M tokens | Output / 1M tokens | Monthly tokens | Monthly cost |
|---|---|---|---|---|---|---|
| CEO / Strategy | Claude Sonnet 4.6 | Anthropic | $3.00 | $15.00 | 5M in / 1M out | ~$30 |
| Engineering (planned) | Claude Sonnet 4.6 | Anthropic | $3.00 | $15.00 | 25M in / 5M out | ~$150 |
| Engineering (execution) | GPT-5-mini | OpenAI | $0.40 | $1.60 | 50M in / 10M out | ~$36 |
| Engineering (completion) | Qwen3-Coder (local) | Ollama | $0 | $0 | 100M in / 20M out | $0 |
| Research | GPT-5-mini | OpenAI | $0.40 | $1.60 | 15M in / 3M out | ~$11 |
| Marketing / Content | Claude Haiku 4.5 | Anthropic | $0.80 | $4.00 | 10M in / 2M out | ~$16 |
| Customer Support | GPT-5-mini | OpenAI | $0.40 | $1.60 | 30M in / 5M out | ~$20 |
| Finance / Data | DeepSeek V3 | DeepSeek | $0.50 | $2.00 | 5M in / 1M out | ~$5 |
| Voice (STT) | Whisper (local) | Ollama | $0 | $0 | — | $0 |
| Embeddings | text-embedding-3-small | OpenAI | $0.02 | $0 | 10M tokens | ~$0.20 |

### Model Tiers (Cost-Performance Tradeoffs)

| Tier | Models | Cost / 1M in+out | Best for |
|---|---|---|---|
| **Free / Local** | Qwen3-Coder, Llama 4, DeepSeek-Coder-V2 (via Ollama) | $0 | Code completion, embeddings, simple classification |
| **Budget** | GPT-5-mini, Claude Haiku 4.5, Gemini 2.5 Flash | $0.40–4.80 | High-volume: support, research, content drafts |
| **Premium** | Claude Sonnet 4.6, GPT-5, Gemini 2.5 Pro | $3–18 | Core reasoning: planning, code generation, strategy |
| **Expert** | Claude Opus 4.7, GPT-5-ultra | $15–75 | Critical decisions, complex architecture, legal review |

## Monthly Budget Scenarios

### Scenario A: Pure Self-Hosted (Zero API costs — local models only)

| Item | Cost |
|---|---|
| 1× GPU server (RTX 4090) | $250 |
| 1× CPU server (8 vCPU / 32 GB) | $75 |
| Storage (500 GB volume + 1 TB B2 backup) | $15 |
| Domain + DNS + email | $10 |
| **Total** | **~$350/mo** |

**Runs:** Ollama + OpenCode + n8n + Chatwoot + all infra.
**Tradeoff:** Slower, dumber agents. Only Qwen3-Coder / Llama 4 class models.

### Scenario B: Hybrid (Local models + budget API for reasoning)

| Item | Cost |
|---|---|
| 1× CPU server (8 vCPU / 32 GB) | $75 |
| LLM API (Sonnet 4.6 + GPT-5-mini + Haiku) | ~$260 |
| Storage + backup | $15 |
| Domain + DNS + email | $10 |
| **Total** | **~$360/mo** |

**Runs:** Full stack with Sonnet-level reasoning + GPT-5-mini for bulk.
**Tradeoff:** Best cost/performance ratio. Recommended default.

### Scenario C: Full API (No GPU, all cloud models)

| Item | Cost |
|---|---|
| 1× CPU server (8 vCPU / 32 GB) | $75 |
| LLM API (Sonnet 4.6 + GPT-5 + Opus on-demand) | ~$600 |
| Storage + backup | $15 |
| Domain + DNS + email | $10 |
| **Total** | **~$700/mo** |

**Runs:** Maximum intelligence. Opus for critical decisions.
**Tradeoff:** 2× cost for marginal intelligence gain.

### Scenario D: Enterprise (Redundant + staging + SSO + 24/7 support)

| Item | Cost |
|---|---|
| 2× CPU server (production + staging) | $150 |
| 1× GPU server (training + batch inference) | $250 |
| LLM API | ~$800 |
| Storage (HA, replicated) | $40 |
| Domain + DNS + email + monitoring | $25 |
| **Total** | **~$1,265/mo** |

## Per-Department Breakdown (Scenario B — Recommended)

| Department | LLM Cost | Server Share | Storage | Total |
|---|---|---|---|---|
| CEO / Strategy | $30 | $5 | — | $35 |
| Engineering | $186 | $15 | $2 | $203 |
| Research | $11 | $5 | — | $16 |
| Customer Support | $20 | $5 | $1 | $26 |
| Marketing | $16 | $3 | $1 | $20 |
| Finance / Data | $5 | $3 | $3 | $11 |
| Voice | $0 | $2 | — | $2 |
| Infrastructure | — | $20 | $8 | $28 |
| **Total** | **$268** | **$58** | **$15** | **~$341** |

## One-Time Setup Costs

| Item | Cost |
|---|---|
| Domain registration (1 year) | $10–20 |
| SSL via Caddy/LetsEncrypt | $0 |
| Initial infrastructure config (time) | ~4–8 hours |
| Model weights download (70B model) | ~$0 (bandwidth) |
| **Total one-time** | **~$20** |

## Cost-Saving Tips

1. **Use OpenCode's built-in models** for free-tier development before committing to API keys
2. **Route all code completion through local Ollama** (Qwen3-Coder) — saves 80% of Engineering API costs
3. **Use GPT-5-mini for classification/summarization** — Sonnet is overkill for structure-only tasks
4. **Cache common LLM responses** via Mem0 — reduces repeat API calls by 40–60%
5. **Use OpenRouter** — one key for 200+ models, automatic fallback on rate limits, pay-per-token
6. **Pin to cheaper models in n8n workflows** — use Haiku/GPT-5-mini for automation, not Sonnet
7. **Set per-user daily token budgets** in Open WebUI to prevent runaway costs
8. **Run batch inference on GPU server overnight** for content generation (cheaper than API)
