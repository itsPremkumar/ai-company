# Integration Map — Data Flow & Tool Wiring

> How every tool in the AI-Operated Company connects.
> Arrows show data flow direction: `Source → Destination`.

## High-Level Architecture

```
                     ┌─────────────────┐
                     │   Open WebUI    │ ← Human interface
                     │   Mattermost    │ ← Agent-human chat
                     └────────┬────────┘
                              │
                     ┌────────▼────────┐
                     │   Hermes Agent  │ ← CEO brain
                     │   (CEO / CTO)   │
                     └────────┬────────┘
                              │
          ┌───────────────────┼───────────────────┐
          ▼                   ▼                   ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   Agent-Reach   │ │   OpenHands     │ │  CrewAI / AGNO  │
│   (Research)    │ │   OpenCode      │ │  (Orchestration)│
│   Crawl4AI      │ │   (Engineering) │ │  LangGraph      │
│   Firecrawl     │ │   MetaGPT       │ │                 │
└────────┬────────┘ └────────┬────────┘ └────────┬────────┘
         │                   │                   │
         └───────────────────┼───────────────────┘
                             ▼
                    ┌─────────────────┐
                    │     n8n         │ ← Workflow glue
                    │  (Automation)   │
                    └────────┬────────┘
                             │
          ┌───────────────────┼───────────────────┐
          ▼                   ▼                   ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   Airbyte       │ │   Chatwoot      │ │   Mautic        │
│   (Data Sync)   │ │   (Support)     │ │   (Marketing)   │
│                 │ │                 │ │                 │
└────────┬────────┘ └────────┬────────┘ └────────┬────────┘
         │                   │                   │
         ▼                   ▼                   ▼
┌─────────────────────────────────────────────────────────┐
│                    PostgreSQL + pgvector                  │
│               (All tools → single data lake)              │
└────────────────────────┬────────────────────────────────┘
                         │
          ┌──────────────┴──────────────┐
          ▼                             ▼
┌─────────────────┐           ┌─────────────────┐
│   Grafana       │           │   Kopia         │
│   (Dashboards)  │           │   (Backup)      │
│   Prometheus    │           │   MinIO         │
│   Loki          │           │   (Storage)     │
└─────────────────┘           └─────────────────┘
```

## Data Flow by Department

### 1. Core Intelligence (Brain)

```
Hermes Agent
  ├─ Reads from: Mem0 (memory), Graphiti (knowledge graph), PostgreSQL
  ├─ Writes to: Mem0, Graphiti, PostgreSQL, n8n (workflow triggers)
  ├─ Delegates to: Agent-Reach (research), OpenHands (coding), CrewAI (multi-agent)
  └─ Communicates via: Mattermost (agent-human), n8n (cross-service)
```

### 2. Research & Intelligence

```
Agent-Reach
  ├─ Reads from: SearXNG (private web), Crawl4AI (scraped pages)
  ├─ Writes to: PostgreSQL (structured research), Mem0 (memory)
  └─ Feeds: Hermes Agent (insights), Mautic (lead data)

Crawl4AI / Firecrawl
  ├─ Reads from: Public web / target URLs
  ├─ Writes to: PostgreSQL (raw content), MinIO (screenshots/PDFs)
  └─ Feeds: Docling (document parsing → structured data → PostgreSQL)
```

### 3. Engineering

```
OpenCode
  ├─ Reads from: Git repos (Gitea/Forgejo), PostgreSQL (schema/docs)
  ├─ Writes to: Git repos (code), MinIO (build artifacts), PostgreSQL (logs)
  └─ Feeds: OpenHands (complex tasks → handoff), Superplane (tracking)

OpenHands
  ├─ Reads from: Git repos, issue trackers, OpenCode output
  ├─ Writes to: Git repos, Docker registry, Coolify (deployment trigger)
  └─ Feeds: Hermes (review → deploy decision)

Coolify
  ├─ Reads from: Git repos (auto-deploy hooks), Docker registry
  ├─ Writes to: Docker containers, Prometheus (metrics)
  └─ Monitored by: Grafana (deploy health)
```

### 4. Customer Support

```
Chatwoot
  ├─ Reads from: PostgreSQL (conversations), Open WebUI (AI knowledge base)
  ├─ Writes to: PostgreSQL (tickets), n8n (support workflows)
  └─ Feeds: Hermes (escalations), ERPNext (billing tickets)

n8n (Support workflows)
  ├─ Reads from: Chatwoot webhooks, PostgreSQL
  ├─ Writes to: ERPNext (tickets → invoices), Mautic (campaign triggers)
  └─ Automation: Auto-reply, ticket routing, SLA tracking
```

### 5. Marketing

```
Mautic
  ├─ Reads from: PostgreSQL (contacts), Agent-Reach (lead data), Formbricks (survey responses)
  ├─ Writes to: PostgreSQL (campaigns), Mail server (Postal/Mailcow)
  └─ Feeds: Grafana (campaign metrics), ERPNext (lead → opportunity)

Formbricks
  ├─ Reads from: PostgreSQL (surveys), Open WebUI (user segments)
  ├─ Writes to: PostgreSQL (responses), n8n (trigger campaigns)
  └─ Feeds: Mautic (campaign triggers), PostHog (product analytics)
```

### 6. Finance & Data

```
ERPNext
  ├─ Reads from: PostgreSQL (transactions), Airbyte (synced SaaS data)
  ├─ Writes to: PostgreSQL (ledger, invoices), MinIO (documents)
  └─ Feeds: Grafana (financial dashboards), Hermes (CFO reports)

Airbyte
  ├─ Reads from: 600+ connector sources (Stripe, ERPNext, Chatwoot, Mautic, PostgreSQL)
  ├─ Writes to: PostgreSQL (central data lake), Meilisearch (search index)
  └─ Feeds: Grafana (BI dashboards), Metabase (reports)

PostgreSQL + pgvector
  ├─ Central data lake: ALL tools write here
  ├─ Embeddings stored in: pgvector (for RAG, semantic search)
  └─ Consumed by: Open WebUI (RAG), Mem0 (memory extraction), Meilisearch (full-text)
```

### 7. Voice / Telecalling

```
Pipecat
  ├─ Reads from: LiveKit (audio stream), Whisper (STT → text), PostgreSQL (knowledge base)
  ├─ Writes to: LiveKit (audio response), Piper (TTS), PostgreSQL (transcripts)
  └─ Feeds: n8n (call summaries → ERPNext), Chatwoot (support tickets)

Asterisk / FreeSWITCH
  ├─ Reads from: SIP trunk, call routing config
  ├─ Writes to: LiveKit (bridged audio), PostgreSQL (CDR logs)
  └─ Feeds: Pipecat (AI processing → response)
```

### 8. Observability

```
Prometheus
  ├─ Scrapes: All Docker services, node exporter, Coolify
  ├─ Writes to: Prometheus TSDB, Alertmanager
  └─ Feeds: Grafana (dashboards), n8n (auto-remediation)

Grafana
  ├─ Reads from: Prometheus (metrics), Loki (logs), PostgreSQL (business data)
  ├─ Dashboards: System health, API costs, department KPIs, business metrics
  └─ Alerts: To Mattermost (ops channel), n8n (auto-remediation)
```

### 9. SSO / Identity

```
Keycloak
  ├─ Authenticates: All web services (Grafana, n8n, Open WebUI, Mattermost, Chatwoot, etc.)
  ├─ Reads from: PostgreSQL (users, sessions), LDAP (if needed)
  ├─ Writes to: PostgreSQL (auth events, sessions)
  └─ Policies: RBAC per department, 2FA for admin, API token management
```

### 10. Backup

```
Kopia
  ├─ Reads from: All Docker volumes (PostgreSQL, MinIO, Grafana, etc.)
  ├─ Writes to: MinIO (local backup), Backblaze B2 (offsite)
  └─ Schedule: Hourly snapshots, daily retention (30d), weekly archive (12mo)

PostgreSQL backup (pg_dump + Kopia)
  ├─ Writes: Daily SQL dump → Kopia snapshot → MinIO + B2
  └─ Verification: Monthly restore test → separate staging environment
```

## Critical Integration Paths (Must Work End-to-End)

### Path 1: Lead → Sale → Invoice

```
Agent-Reach (discover lead)
  → PostgreSQL (store lead)
  → n8n (enrich + score)
  → Mautic (nurture campaign)
  → Chatwoot (sales conversation)
  → ERPNext (create opportunity → quote → invoice)
  → PostgreSQL (transaction complete)
  → Grafana (revenue dashboard updates)
```

### Path 2: Bug Report → Fix → Deploy

```
Chatwoot (customer bug report)
  → n8n (create issue in Gitea)
  → OpenHands (analyze + fix code)
  → OpenCode (review + test)
  → Coolify (deploy to staging → production)
  → Mattermost (notify team in ops channel)
  → Chatwoot (auto-reply to customer: fixed)
```

### Path 3: Research Insight → Content → Campaign

```
Agent-Reach (research topic)
  → Hermes (validate + prioritize)
  → n8n (trigger content pipeline)
  → Automated-Video-Generator (produce video)
  → Mautic (schedule campaign)
  → Mattermost (CMO reviews)
  → Mautic (send → track → report)
  → Grafana (campaign dashboard)
```

### Path 4: Customer Query → Resolution

```
Chatwoot (incoming query)
  → Open WebUI RAG (search knowledge base)
  → AI auto-reply (if confidence > 90%)
  → Or: Pipecat (voice call if urgent)
  → Or: n8n (escalate to human)
  → ERPNext (ticket → invoice if billable)
  → PostgreSQL (update customer history)
  → Mem0 (remember for next interaction)
```

## Webhook / API Integration Table

| Source | Trigger | Target | Payload |
|---|---|---|---|
| Chatwoot | New conversation | n8n | Customer info, message, source |
| Gitea | New issue / PR | n8n | Repo, title, body, author |
| ERPNext | New sales order | n8n | Customer, items, amount |
| Mautic | Campaign action | n8n | Contact, event, campaign |
| Formbricks | Survey response | n8n | Respondent, answers, score |
| Stripe | New payment | n8n → Airbyte | Amount, customer, invoice |
| Mattermost | Slash command | n8n | User, command, args |
| Grafana | Alert fired | n8n → Mattermost | Alert name, severity, graph |
| Keycloak | User event | n8n | Event type, user, IP |
| Kopia | Backup completed | n8n → Mattermost | Status, duration, size |
