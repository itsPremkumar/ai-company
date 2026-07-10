# 🚀 Quickstart — Build the AI Company (concrete first steps)

> The docs describe tools. This file says WHAT TO DO FIRST. Start small, expand later.

## Phase 0 — Prerequisites (one-time)
1. Install **Docker** + **Docker Compose** (everything runs in containers).
2. Get a capable LLM API key (or run a local model via Ollama + Open WebUI).
3. Create a project folder: `~/ai-company/` (this folder).

## Phase 1 — The 7-Agent MVP (week 1)
Stand up ONLY the spine. Use the verified core:
| Agent | Tool | Why |
|---|---|---|
| AI CEO | `claw-empire` | Command desk |
| AI COO | `markus` | Loop runner |
| AI Research | `Agent-Reach` | Web intelligence |
| AI SWE | `OpenHands` + Hermes | Build |
| AI Marketing | `Mautic` + Agent-Reach | Reach |
| AI Sales/CRM | `NocoBase` | Leads |
| AI CFO | `ERPNext` | Finance |

→ Product to sell first: **your `Automated-Video-Generator`** (via its MCP server).

## Phase 2 — Memory + Brain (week 2)
- Add **Mem0** (memory) + **pgvector** (vectors) + **Graphiti** (knowledge graph).
- Wire them so Hermes retains learnings across sessions → enables self-evolution.

## Phase 3 — Infrastructure backbone (week 3)
Deploy the `COMPULSORY_BASELINE.md` 20-set:
Keycloak, Infisical, PostgreSQL, MinIO, Docker+Coolify, Prometheus+Grafana+Loki, NATS,
ERPNext, Postal+Listmonk, Outline+OpenWebUI, n8n, Chatwoot, Matomo, Gitea+Forgejo, Plane, Wazuh.

## Phase 4 — Expand by domain
- Add `departments/21-ecommerce.md` (Medusa) if selling products.
- Add `departments/20-gap-fillers.md` tools as needed (legal, translation, scheduling).
- Add `departments/22-self-evolving-core.md` layer (AgentZero for autonomy).

## ⚠️ Principles
- **Don't deploy all 60 departments at once.** Ship the 7-agent MVP, prove it earns, then expand.
- **Verify before trusting:** for every `(canonical)` repo, check stars/maintenance/license live
  before production use (GitHub API was rate-limited when this folder was built).
- **Self-evolution is research-grade:** Hermes + Mem0 is the practical starting point; AgentZero
  adds autonomy. Combine, don't bet on one.
- **Keep it $0 software cost:** every tool here is open-source/self-hostable. Compute (VPS/GPU) is
  the only bill.

## Next actions for the human owner
- [ ] Commit this folder to git.
- [ ] Pick Product #1 (recommend: Video-Generator).
- [ ] Stand up Phase 1 (7-agent MVP) on a VPS.
- [ ] Re-verify `(canonical)` star counts once API limit clears.
