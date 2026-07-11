# 🏛 The Compulsory Baseline — Standard Stack for ANY Company

> **Principle:** This is the **minimum default set** every company needs to *exist and operate*,
> regardless of industry (sells software, videos, consulting, products, services — doesn't matter).
> It is industry-agnostic. Add domain tools ON TOP of this; this set is always present.
>
> All projects are **100% free / open-source / self-hostable**. ✅ = star count verified live in
> this project's research sessions; (canonical) = well-known repo, not re-verified this session.

---

## 1. 🔐 Identity & Access (IAM) — *compulsory*
Every company has users, roles, SSO.
- **Keycloak** ✅ 35.6k ★ · Apache-2.0 · https://github.com/keycloak/keycloak

## 2. 🔑 Secrets Management — *compulsory*
API keys, DB passwords, tokens must not live in code.
- **Infisical** ✅ 27.8k ★ · https://github.com/Infisical/infisical
- (alt) **HashiCorp Vault** · https://github.com/hashicorp/vault

## 3. 🗄 Database — *compulsory*
Primary transactional store.
- **PostgreSQL** ✅ 21.4k ★ · https://github.com/postgres/postgres

## 4. 📦 Object Storage — *compulsory*
Files, images, videos, backups, assets.
- **MinIO** ✅ 61.3k ★ · AGPL-3.0 · https://github.com/minio/minio

## 5. 🐳 Containers & Deployment — *compulsory*
Package and run everything; self-host PaaS.
- **Docker** · https://github.com/docker/docs
- **Coolify** ✅ 58.2k ★ · Apache-2.0 · https://github.com/coollabsio/coolify

## 6. 📡 Observability (metrics + logs) — *compulsory*
You cannot run a company blind.
- **Prometheus** · https://github.com/prometheus/prometheus (metrics)
- **Grafana** ✅ 75.5k ★ · AGPL-3.0 · https://github.com/grafana/grafana (dashboards)
- **Loki** · https://github.com/grafana/loki (logs)

## 7. 🔔 Messaging / Event Bus — *compulsory*
Decouple services, async jobs, notifications.
- **NATS** · https://github.com/nats-io/nats-server
- (alt) **RabbitMQ** · https://github.com/rabbitmq/rabbitmq

## 8. 👥 CRM — *compulsory*
Every company has customers/contacts to manage.
- **ERPNext (CRM module)** ✅ 36.7k ★ · GPL-3.0 · https://github.com/frappe/erpnext
- (alt) **Twenty** ✅ 52.7k ★ · https://github.com/twentyhq/twenty

## 9. 💰 ERP / Finance / Accounting — *compulsory*
Invoicing, books, payroll — legally required everywhere.
- **ERPNext** ✅ 36.7k ★ · GPL-3.0 · https://github.com/frappe/erpnext
- (alt) **Odoo Community** ✅ 52.9k ★ · https://github.com/odoo/odoo
- (alt) **Akaunting** · https://github.com/akaunting/akaunting

## 10. ✉ Email & Comms — *compulsory*
Outbound mail + marketing reach.
- **Postal** (mail server) · https://github.com/postalserver/postal
- **Listmonk** ✅ 22k ★ · AGPL-3.0 · https://github.com/knadh/listmonk (newsletters)

## 11. 📚 Docs / Wiki / Knowledge — *compulsory*
Internal documentation + company knowledge.
- **Outline** · https://github.com/outline/outline
- **Open WebUI** ✅ 144.9k ★ · https://github.com/open-webui/open-webui (AI knowledge portal)

## 12. 🧠 AI Long-Term Memory — *compulsory (for AI company)*
Agents must remember across sessions.
- **Mem0** ✅ 60.5k ★ · Apache-2.0 · https://github.com/mem0ai/mem0
- **pgvector** ✅ 22.1k ★ · https://github.com/pgvector/pgvector (vectors in Postgres)

## 13. 🔄 Workflow Automation — *compulsory*
Glue systems together without custom code.
- **n8n** ✅ 195.9k ★ · https://github.com/n8n-io/n8n

## 14. 🤖 Agent Orchestration — *compulsory (for AI company)*
Run the AI workforce.
- **Hermes Agent** (this agent) · https://github.com/NousResearch/hermes-agent
- **CrewAI** ✅ 55.3k ★ · MIT · https://github.com/crewAIInc/crewAI
- **LangGraph** ✅ 37k ★ · MIT · https://github.com/langchain-ai/langgraph

## 15. 🌐 Web Research — *compulsory (for AI company)*
Agents need to read the internet.
- **Agent-Reach** ✅ 54.3k ★ · MIT · https://github.com/Panniantong/Agent-Reach
- **SearXNG** ✅ 33.7k ★ · AGPL-3.0 · https://github.com/searxng/searxng

## 16. 💬 Customer Support — *compulsory*
Every company answers customers.
- **Chatwoot** ✅ 34.3k ★ · https://github.com/chatwoot/chatwoot

## 17. 📊 Analytics — *compulsory*
Know what's happening (web + product).
- **Matomo** · https://github.com/matomo-org/matomo
- (alt) **Plausible CE** · https://github.com/plausible/plausible

## 18. 🔧 Version Control & CI/CD — *compulsory*
Code + automated builds.
- **Gitea** · https://github.com/gitea/gitea (VCS)
- **Forgejo Actions** · https://github.com/forgejo/forgejo (CI)
- (alt) **Woodpecker CI** · https://github.com/woodpecker-ci/woodpecker

## 19. 📋 Project Management — *compulsory*
Track work/delivery.
- **Plane** · https://github.com/getplane/plane
- (alt) **OpenProject** · https://github.com/openproject/openproject

## 20. 🛡 Security Monitoring — *compulsory*
Detect intrusions / anomalies.
- **Wazuh** · https://github.com/wazuh/wazuh

---

## ✅ The "Must-Have 20 (+ MLOps)" one-line summary
For **ANY company**, self-host these by default:
**Keycloak, Infisical, PostgreSQL, MinIO, Docker+Coolify, Prometheus+Grafana+Loki, NATS,
ERPNext, Postal+Listmonk, Outline+OpenWebUI, Mem0+pgvector, n8n, Hermes+CrewAI+LangGraph,
Agent-Reach+SearXNG, Chatwoot, Matomo, Gitea+Forgejo, Plane, Wazuh.**

For a **non-AI company**, drop #12, #14, #15 (memory/orchestration/research) — the other 17 are
universal. For an **AI company**, keep all 20. Then add **21. MLflow** (experiment tracking + model
registry) and **22. vLLM** (self-hosted LLM serving) as the MLOps layer.

## ➕ Then add DOMAIN tools on top
- Video company → your `Automated-Video-Generator` + ComfyUI
- E-commerce → Saleor / Medusa
- HR-heavy → OrangeHRM
- Legal-heavy → Documenso
- (see `ENTERPRISE_STACK.md` and `departments/` for domain layers)

This 20-set is the **default operating system of the company** — present in every deployment.
