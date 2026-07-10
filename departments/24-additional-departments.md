# ➕ Additional Departments (gaps from the 60-team list)

> These departments appeared in the original 60+ list but were NOT yet given a dedicated section.
> Each maps to a free/open-source project. Kept in one file to avoid 13 micro-files; cross-referenced
> from the MASTER_INDEX. Functions already covered elsewhere are noted, not duplicated.

## 🔓 Open Source Program Office (OSPO) — *critical for an OSS-native company*
Your entire stack is open-source; you MUST manage contributions, licensing, community.
- **TODO Group / OSPO** (guidance) · https://github.com/todogroup/ospo
- **Hydrosphere / ossls** (license scanning) · https://github.com/hydrospheredata/ossls
- **FOSSA** (OSS compliance) · https://github.com/fossas/fossa-cli
- Integration: governs `Automated-Video-Generator` + all forked tools; tracks licenses (e.g., AGPL
  vs MIT obligations).

## 🤝 Business Development & Partnerships
Strategic growth, external collaborations, integrations.
- `crewAIInc/crewAI` (role: BD Agent) · https://github.com/crewAIInc/crewAI
- `enosis-ai/agent-commerce` (agent-to-agent commerce, emerging) · (canonical)
- Integration: BD agent uses Agent-Reach to find partners → NocoBase tracks → ERPNext contracts.

## 📣 Public Relations (PR)
Media outreach, press, public communication.
- `mautic/mautic` (PR campaigns) · https://github.com/mautic/mautic
- `Agent-Reach` (media monitoring) · https://github.com/Panniantong/Agent-Reach
- Integration: PR agent monitors coverage via Agent-Reach → pitches via Mautic → reports to CEO.

## 😊 Customer Success (retention)
Distinct from Support (break/fix). Proactive retention, onboarding, health scores.
- `chatwoot/chatwoot` (success + support) · https://github.com/chatwoot/chatwoot
- `metabase/metabase` (health dashboards) · https://github.com/metabase/metabase
- Integration: Success agent tracks account health in Metabase → nudges via Chatwoot → ERPNext renewals.

## 🗄 Database Administration
DB optimization, backups, performance.
- `postgres/postgres` + `pgvector/pgvector` · https://github.com/postgres/postgres
- `pgAdmin` · https://github.com/pgadmin-org/pgadmin4
- `infisical/infisical` (DB secret rotation) · https://github.com/Infisical/infisical
- Integration: DBA agent automates backups/vacuum via Coolify cron + monitors in Grafana.

## 🌐 Network Engineering
Networking, connectivity, zero-trust.
- `openziti/ziti` (zero-trust networking) · https://github.com/openziti/ziti
- `nginx/nginx` (reverse proxy) · https://github.com/nginx/nginx
- Integration: Net agent configures Ziti tunnels + Nginx; monitored via Prometheus.

## 🛒 Procurement
Vendor sourcing, license purchasing, asset inventory.
- `frappe/erpnext` (Purchase module) · https://github.com/frappe/erpnext
- `snipe/snipe-it` (asset management) · https://github.com/snipe/snipe-it
- Integration: Procurement agent sources via Agent-Reach → ERPNext PO → Snipe-IT tracks assets.

## ⚠️ Risk Management
Business risk assessment, continuity.
- `opencybersecurity/risk` (open risk frameworks) · (canonical)
- Integration: Risk agent reviews audit logs (Wazuh) + finance (ERPNext) → reports to CEO/Compliance.

## 🔍 Internal Audit
Process auditing, compliance checks.
- `wazuh/wazuh` (audit logs) · https://github.com/wazuh/wazuh
- `keycloak/keycloak` (access audits) · https://github.com/keycloak/keycloak
- Integration: Audit agent runs periodic Wazuh/Keycloak reports → Compliance officer.

## 💼 Investor Relations
Investor communication (relevant if you raise funds).
- `metabase/metabase` (investor dashboards) · https://github.com/metabase/metabase
- `documenso/documenso` (cap-table/term sheets) · https://github.com/documenso/documenso
- Integration: IR agent builds Metabse deck → Documenso signs → sends to investors.

## 🎓 Learning & Development
Employee/contractor training (agent-light until you hire humans).
- `libretranslate/libretranslate` (course translation) · https://github.com/LibreTranslate/LibreTranslate
- `documenso/documenso` (certificates) · https://github.com/documenso/documenso
- Integration: L&D agent curates docs (Outline) → translates → issues certs.

## ♿ Accessibility
Accessibility (a11y) compliance for all products.
- `getfoobar/axe-core` (a11y testing) · https://github.com/dequelabs/axe-core
- `nvaccess/nvda` (screen-reader testing) · https://github.com/nvaccess/nvda
- Integration: A11y agent runs axe-core in CI → blocks non-compliant releases.

## 🚨 Incident Response
Security/operational incident handling (distinct from SOC monitoring).
- `wazuh/wazuh` (detection) · https://github.com/wazuh/wazuh
- `grafana/loki` + `grafana/oncall` (alerting) · https://github.com/grafana/oncall
- Integration: IR agent gets Loki/OnCall alerts → runs Wazuh playbooks → posts to Chatwoot status.

## 📋 Coverage status of original 60-department list
| Function | Status |
|---|---|
| Executive, Ops, PMO, Product, Eng, R&D, AI/ML, Design, DevOps, QA, Data/BI, Marketing, Sales, CRM, Support, Voice, HR/Legal, Finance, Security, Specialized AI | ✅ Covered (00–17) |
| Video Gen, Infra, Gap-fillers, Ecommerce, Self-evolving, Products | ✅ Covered (18–23) |
| **OSPO, BD/Partnerships, PR, Customer Success, DB Admin, Network, Procurement, Risk, Audit, Investor Rel, L&D, Accessibility, Incident Response** | ⚠️ **Now covered here (24)** |
| Disaster Recovery, Branding, Compliance, Biz Analysis, Innovation Lab | ✅ Folded into Infra / Marketing / Legal / Research already |

All 60+ departments now have a home.
