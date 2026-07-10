# Rollout Roadmap — AI-Operated Company

> Phased approach: start lean, validate, expand. Each phase takes ~1 month.

## Phase 0: Foundation (Days 1–3)

**Goal:** Infrastructure ready. No AI agents yet.

```
[ ] Provision server (Hetnzer/OVH — 8 vCPU / 32 GB / 500 GB)
[ ] Install Docker + Docker Compose
[ ] Configure firewall (80, 443, SSH only)
[ ] Set up DNS + Caddy reverse proxy with auto-TLS
[ ] Deploy PostgreSQL + MinIO + Keycloak
[ ] Configure Keycloak realm + SSO clients
[ ] Deploy Grafana + Prometheus + Loki
[ ] Set up Kopia backups (hourly → MinIO, daily → B2)
[ ] Create Mattermost team + invite users
[ ] Copy .env with strong passwords
```

**Check:** `curl https://auth.yourdomain.com` returns Keycloak login page.

---

## Phase 1: 7-Agent MVP (Month 1)

**Goal:** Core business loop works — research → engineering → deploy.

### Week 1–2: Brain + Research

```
[ ] Install OpenCode (npm i -g opencode-ai)
[ ] Install Agent-Reach (npm i -g agent-reach)
[ ] Configure LLM API keys (OpenRouter or Anthropic)
[ ] Install Mem0 (pip install mem0)
[ ] Run OpenCode `/init` on repo
[ ] Test: "Research competitors in X market" → Agent-Reach returns report
[ ] Test: "Implement feature Y" → OpenCode writes + tests code
[ ] Deploy Coolify → connect to Git repos → auto-build
```

### Week 3–4: Customer-Facing

```
[ ] Deploy Chatwoot → configure inbound email + web widget
[ ] Deploy Open WebUI → point to PostgreSQL + enable RAG
[ ] Deploy n8n → create 3 core workflows:
     1. Chatwoot ticket → Mattermost ops channel
     2. Git push → Coolify deploy
     3. Daily Kopia backup report → Mattermost
[ ] Test: Customer sends email → Chatwoot → AI auto-reply
[ ] Test: Code commit → Coolify auto-deploy → Grafana health check
[ ] Set up Grafana dashboard: system health, ticket volume, deploy status
```

**MVP Checklist:**
- [ ] Research agent finds leads/customers
- [ ] Coding agent ships features
- [ ] Support agent handles basic queries
- [ ] n8n connects the three
- [ ] Backups running + verified
- [ ] Grafana shows business metrics

---

## Phase 2: Growth (Month 2)

**Goal:** Full automation — marketing, sales, finance, voice.

### Week 1–2: Marketing + Sales

```
[ ] Deploy Mautic → import contacts from Chatwoot
[ ] Deploy Formbricks → create NPS + onboarding surveys
[ ] Deploy Meilisearch → index docs + knowledge base
[ ] Connect n8n:
     1. Formbricks response → Mautic campaign trigger
     2. Chatwoot resolved ticket → Mautic nurture sequence
     3. Agent-Reach lead → Mautic contact → email sequence
[ ] Deploy Airbyte → sync Chatwoot + Mautic + ERPNext → PostgreSQL
[ ] Test: Weekly marketing report auto-generated in Grafana
```

### Week 3–4: Finance + Voice

```
[ ] Deploy ERPNext → configure accounting, invoicing, inventory
[ ] Connect n8n:
     1. Chatwoot billing ticket → ERPNext invoice
     2. Mautic campaign → track ROI in ERPNext
[ ] Deploy Pipecat + LiveKit → configure inbound call routing
[ ] Connect Asterisk/FreeSWITCH → Pipecat → voice AI agent
[ ] Test: Customer calls → AI handles query → creates ERPNext ticket
[ ] Set up Kopia backup for ERPNext database
```

**Growth Checklist:**
- [ ] Marketing campaigns running on auto-pilot
- [ ] Customer survey loop active
- [ ] Data pipeline syncs all tools daily
- [ ] ERP tracks income/expenses automatically
- [ ] Voice agent handles basic calls
- [ ] Feature flags (Unleash) enabled for safe rollouts

---

## Phase 3: Scale (Month 3+)

**Goal:** Optimize, add redundancy, increase autonomy.

### Week 1–2: Intelligence + Memory

```
[ ] Deploy OpenOPC → configure Company Mode with org chart
[ ] Hire AI employees into OpenOPC roles
[ ] Enable Self-Grown learning (organizational memory)
[ ] Connect OpenOPC → OpenCode → execution agents
[ ] Set up Mem0 → Hermes → Open WebUI (memory RAG bridge)
[ ] Add Graphiti (temporal knowledge graph) for long-term facts
[ ] Test: "Run the full sales cycle" — OpenOPC orchestrates end-to-end
```

### Week 3–4: Hardening

```
[ ] Add staging environment (clone Phase 1 stack)
[ ] Configure Blue/Green deployments via Coolify
[ ] Set up Unleash feature flags for all services
[ ] Write security hardening checklist (run monthly)
[ ] Configure Grafana alerts → Mattermost ops channel
[ ] Set up cost alerts (LLM API budget caps)
[ ] Add fail2ban + CrowdSec for WAF
[ ] Run restore drill: Kopia backup → staging restore → verify
[ ] Create runbooks for top 10 failure modes
```

### Ongoing Optimization

```
Weekly:
  [ ] Review LLM token usage → adjust model tier per department
  [ ] Review Kopia backup logs → verify integrity
  [ ] Grafana sprint dashboard review

Monthly:
  [ ] Rotate API keys + passwords
  [ ] Audit Keycloak users + permissions
  [ ] Run Docker version upgrades
  [ ] Review Airbyte sync status

Quarterly:
  [ ] Full disaster recovery drill (simulate server loss)
  [ ] Update model providers (new models launch constantly)
  [ ] Re-evaluate tool stack (replace weak projects)
  [ ] Cost optimization audit
```

---

## Decision Gates

| Gate | Trigger | Go/No-Go Criteria |
|---|---|---|
| **Phase 0→1** | Infrastructure green | All services healthy, SSO works, backups running |
| **Phase 1→2** | 30 days elapsed | Customer support agent handles 50%+ queries, 3 n8n workflows running, cost <$400/mo |
| **Phase 2→3** | 60 days elapsed | Marketing campaigns running on auto, ERP tracking real transactions, <$800/mo total |
| **Phase 3+** | 90 days elapsed | OpenOPC running company mode, 2+ AI employees deployed, <$1,500/mo total |

---

## Failure Mode Runbook

| Symptom | Likely Cause | Action |
|---|---|---|
| **OpenCode times out** | LLM API rate limit | Switch model tier down, check OpenRouter billing |
| **n8n workflow stuck** | Webhook target down | Check target service health, retry webhook |
| **PostgreSQL slow** | Query bloat | Run `VACUUM ANALYZE`, check pg_stat_activity, consider read replica |
| **Keycloak login fails** | SSL cert expired | Run `docker compose restart caddy`, check cert renewal |
| **Chatwoot not receiving email** | MX/DNS config | Check SPF/DKIM/DMARC, verify mail server config |
| **Grafana shows gaps** | Prometheus target down | `docker compose logs prometheus`, restart target service |
| **Kopia backup fails** | Storage full | Clean old snapshots, add storage volume |
| **LLM cost spike** | Agent runaway loop | Check token usage per agent, set max_tokens caps, enable approval gates |
| **Coolify deploy hangs** | Docker image build fail | `docker compose logs coolify`, check build logs, rebuild image |
| **Mattermost alerts silent** | Webhook misconfig | Test webhook URL, check Mattermost integrations page |
