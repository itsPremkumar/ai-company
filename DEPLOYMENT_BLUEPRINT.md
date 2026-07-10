# Deployment Blueprint — Core 20 Docker Stack

> Opinionated Docker Compose config for self-hosting the AI-Operated Company.
> Hardware minimum: 8 vCPU / 32 GB RAM / 200 GB SSD. Recommended: 16 vCPU / 64 GB / 500 GB SSD.

## Quickstart

```bash
git clone https://github.com/your-org/ai-company-deploy
cd ai-company-deploy

# 1. Set environment (edit .env first)
cp .env.example .env
nano .env

# 2. Launch core infrastructure
docker compose -f compose.core.yml up -d

# 3. Launch application layer (after core is healthy)
docker compose -f compose.apps.yml up -d

# 4. Verify health
docker compose ps
curl http://localhost:9090/-/healthy  # Prometheus health
```

## Hardware Tiers

| Tier | vCPU | RAM | Storage | Monthly (Hetzner/OVH) | Runs |
|---|---|---|---|---|---|
| **MVP** | 4 | 16 GB | 200 GB | ~$40 | Core DBs + n8n + Chatwoot + Mautic + Open WebUI |
| **Growth** | 8 | 32 GB | 500 GB | ~$80 | All core 20 + Grafana + Loki + Meilisearch |
| **Scale** | 16 | 64 GB | 1 TB | ~$160 | Everything + redundancy + staging environment |

## Core Infrastructure (`compose.core.yml`)

### 1. PostgreSQL + pgvector

```yaml
services:
  postgres:
    image: pgvector/pgvector:pg17
    restart: unless-stopped
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: ${PG_PASSWORD}
      POSTGRES_DB: ai_company
    ports:
      - "5432:5432"
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
    deploy:
      resources:
        limits:
          memory: 2G
```

### 2. MinIO (S3-compatible object storage)

```yaml
  minio:
    image: minio/minio:latest
    command: server /data --console-address ":9001"
    restart: unless-stopped
    volumes:
      - minio_data:/data
    environment:
      MINIO_ROOT_USER: ${MINIO_ROOT_USER:-minioadmin}
      MINIO_ROOT_PASSWORD: ${MINIO_ROOT_PASSWORD}
    ports:
      - "9000:9000"
      - "9001:9001"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
```

### 3. Keycloak (IAM / SSO)

```yaml
  keycloak:
    image: quay.io/keycloak/keycloak:latest
    command: start --proxy edge
    restart: unless-stopped
    volumes:
      - keycloak_data:/opt/keycloak/data
    environment:
      KC_DB: postgres
      KC_DB_URL: jdbc:postgresql://postgres:5432/keycloak
      KC_DB_USERNAME: postgres
      KC_DB_PASSWORD: ${PG_PASSWORD}
      KEYCLOAK_ADMIN: admin
      KEYCLOAK_ADMIN_PASSWORD: ${KC_ADMIN_PASSWORD}
    ports:
      - "8443:8443"
    depends_on:
      postgres:
        condition: service_healthy
```

### 4. Coolify (self-hosted PaaS)

```yaml
  coolify:
    image: ghcr.io/coollabsio/coolify:latest
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - coolify_data:/data
    environment:
      COOLIFY_APP_ID: ${COOLIFY_APP_ID}
      COOLIFY_SECRET_KEY: ${COOLIFY_SECRET_KEY}
      COOLIFY_DATABASE_URL: postgresql://postgres:${PG_PASSWORD}@postgres:5432/coolify
    ports:
      - "8000:8000"
    depends_on:
      postgres:
        condition: service_healthy
```

### 5. n8n (workflow automation)

```yaml
  n8n:
    image: n8nio/n8n:latest
    restart: unless-stopped
    volumes:
      - n8n_data:/home/node/.n8n
    environment:
      N8N_DATABASE_TYPE: postgresdb
      N8N_DATABASE_HOST: postgres
      N8N_DATABASE_PORT: 5432
      N8N_DATABASE_NAME: n8n
      N8N_DATABASE_USER: postgres
      N8N_DATABASE_PASSWORD: ${PG_PASSWORD}
      N8N_BASIC_AUTH_ACTIVE: "true"
      N8N_BASIC_AUTH_USER: admin
      N8N_BASIC_AUTH_PASSWORD: ${N8N_PASSWORD}
    ports:
      - "5678:5678"
    depends_on:
      postgres:
        condition: service_healthy
```

### 6. Grafana + Prometheus + Loki (observability)

```yaml
  prometheus:
    image: prom/prometheus:latest
    restart: unless-stopped
    volumes:
      - ./config/prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    ports:
      - "9090:9090"

  loki:
    image: grafana/loki:latest
    restart: unless-stopped
    volumes:
      - ./config/loki.yml:/etc/loki/local-config.yaml
      - loki_data:/loki
    ports:
      - "3100:3100"

  grafana:
    image: grafana/grafana:latest
    restart: unless-stopped
    volumes:
      - grafana_data:/var/lib/grafana
    environment:
      GF_SERVER_ROOT_URL: https://grafana.${DOMAIN}
      GF_AUTH_GENERIC_OAUTH_ENABLED: "true"
      GF_AUTH_GENERIC_OAUTH_NAME: Keycloak
      GF_AUTH_GENERIC_OAUTH_CLIENT_ID: grafana
      GF_AUTH_GENERIC_OAUTH_CLIENT_SECRET: ${GF_OAUTH_SECRET}
      GF_AUTH_GENERIC_OAUTH_AUTH_URL: https://auth.${DOMAIN}/realms/${KC_REALM}/protocol/openid-connect/auth
      GF_AUTH_GENERIC_OAUTH_TOKEN_URL: https://auth.${DOMAIN}/realms/${KC_REALM}/protocol/openid-connect/token
      GF_AUTH_GENERIC_OAUTH_API_URL: https://auth.${DOMAIN}/realms/${KC_REALM}/protocol/openid-connect/userinfo
    ports:
      - "3000:3000"
    depends_on:
      - prometheus
      - loki
```

## Application Layer (`compose.apps.yml`)

### 7. Open WebUI (knowledge interface)

```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    restart: unless-stopped
    volumes:
      - openwebui_data:/app/backend/data
    environment:
      OLLAMA_BASE_URL: http://ollama:11434
      WEBUI_SECRET_KEY: ${WEBUI_SECRET}
      WEBUI_NAME: AI Company
    ports:
      - "8080:8080"
```

### 8. Ollama (local LLM inference)

```yaml
  ollama:
    image: ollama/ollama:latest
    restart: unless-stopped
    volumes:
      - ollama_data:/root/.ollama
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
    ports:
      - "11434:11434"
```

### 9. SearXNG (private search)

```yaml
  searxng:
    image: searxng/searxng:latest
    restart: unless-stopped
    volumes:
      - ./config/searxng/settings.yml:/etc/searxng/settings.yml:ro
      - ./config/searxng/limiter.toml:/etc/searxng/limiter.toml:ro
      - searxng_data:/etc/searxng
    environment:
      SEARXNG_BASE_URL: https://search.${DOMAIN}
      SEARXNG_SECRET_KEY: ${SEARXNG_SECRET}
    ports:
      - "8888:8080"
```

### 10. Meilisearch (full-text search)

```yaml
  meilisearch:
    image: getmeili/meilisearch:latest
    restart: unless-stopped
    volumes:
      - meili_data:/meili_data
    environment:
      MEILI_MASTER_KEY: ${MEILI_KEY}
      MEILI_ENV: production
    ports:
      - "7700:7700"
```

### 11. Chatwoot (customer support)

```yaml
  chatwoot:
    image: chatwoot/chatwoot:latest
    restart: unless-stopped
    volumes:
      - chatwoot_data:/app/storage
    environment:
      POSTGRES_HOST: postgres
      POSTGRES_DATABASE: chatwoot
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: ${PG_PASSWORD}
      REDIS_URL: redis://redis:6379
      SECRET_KEY_BASE: ${CHATWOOT_SECRET}
      FRONTEND_URL: https://support.${DOMAIN}
    ports:
      - "3001:3000"
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_started
```

### 12. Mattermost (internal chat)

```yaml
  mattermost:
    image: mattermost/mattermost-team-edition:latest
    restart: unless-stopped
    volumes:
      - mattermost_data:/mattermost/data
      - mattermost_config:/mattermost/config
    environment:
      MM_USERNAME: mmuser
      MM_PASSWORD: ${MM_PASSWORD}
      MM_DBNAME: mattermost
      MM_SQLSETTINGS_DATASOURCE: postgres://postgres:${PG_PASSWORD}@postgres:5432/mattermost?sslmode=disable
      MM_SERVICESETTINGS_SITEURL: https://chat.${DOMAIN}
    ports:
      - "8065:8065"
    depends_on:
      postgres:
        condition: service_healthy
```

### 13. Mautic (marketing automation)

```yaml
  mautic:
    image: mautic/mautic:latest
    restart: unless-stopped
    volumes:
      - mautic_data:/var/www/html
    environment:
      MAUTIC_DB_HOST: postgres
      MAUTIC_DB_NAME: mautic
      MAUTIC_DB_USER: postgres
      MAUTIC_DB_PASSWORD: ${PG_PASSWORD}
      MAUTIC_RUN_CRON_JOBS: "true"
      MAUTIC_TRUSTED_HOSTS: ${DOMAIN}
    ports:
      - "8081:80"
    depends_on:
      postgres:
        condition: service_healthy
```

### 14. Airbyte (data pipeline)

```yaml
  airbyte:
    image: airbyte/airbyte:latest
    restart: unless-stopped
    volumes:
      - airbyte_data:/config
    environment:
      AIRBYTE_DB_HOST: postgres
      AIRBYTE_DB_NAME: airbyte
      AIRBYTE_DB_USER: postgres
      AIRBYTE_DB_PASSWORD: ${PG_PASSWORD}
      AIRBYTE_URL: https://airbyte.${DOMAIN}
    ports:
      - "8001:8001"
    depends_on:
      postgres:
        condition: service_healthy
```

## Agent Services (CLI — no Docker image, installed on host)

These tools run as CLI commands, not as Docker services:

| Tool | Install | Runs On | Needs API Key |
|---|---|---|---|
| **OpenCode** | `npm i -g opencode-ai` | Host/CI | 75+ providers supported |
| **OpenHands** | `docker run -d ghcr.io/all-hands-ai/openhands` | Docker (separate) | LLM API key |
| **Agent-Reach** | `npm i -g agent-reach` | Host/CI | GitHub token |
| **Docling** | `pip install docling` | Python venv | — |
| **Crawl4AI** | `pip install crawl4ai` | Python venv | — |
| **Mem0** | `pip install mem0` | Python venv | OpenAI-compatible key |
| **Kopia** | Binary download | Host | S3/MinIO credentials |

## Volumes (all services)

```yaml
volumes:
  pgdata:
  minio_data:
  keycloak_data:
  coolify_data:
  n8n_data:
  prometheus_data:
  loki_data:
  grafana_data:
  openwebui_data:
  ollama_data:
  searxng_data:
  meili_data:
  chatwoot_data:
  mattermost_data:
  mattermost_config:
  mautic_data:
  airbyte_data:
  redis_data:
```

## `.env.example`

```bash
# Domain
DOMAIN=ai-company.example.com

# PostgreSQL
PG_PASSWORD=generate_strong_password_here

# Keycloak
KC_ADMIN_PASSWORD=admin_password
KC_REALM=ai-company

# Coolify
COOLIFY_APP_ID=
COOLIFY_SECRET_KEY=

# MinIO
MINIO_ROOT_PASSWORD=minio_password

# Service Passwords
N8N_PASSWORD=
MM_PASSWORD=
CHATWOOT_SECRET=
WEBUI_SECRET=
SEARXNG_SECRET=
MEILI_KEY=
GF_OAUTH_SECRET=

# External reverse proxy (Caddy or Traefik)
# Recommended: Caddy for automatic HTTPS
CADDY_EMAIL=admin@${DOMAIN}
```

## Reverse Proxy (Caddy)

```yaml
services:
  caddy:
    image: caddy:latest
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - caddy_data:/data
      - caddy_config:/config
```

```caddy
# Caddyfile
{$DOMAIN} {
    reverse_proxy open-webui:8080
}

chat.{$DOMAIN} {
    reverse_proxy mattermost:8065
}

search.{$DOMAIN} {
    reverse_proxy searxng:8080
}

auth.{$DOMAIN} {
    reverse_proxy keycloak:8443
}

support.{$DOMAIN} {
    reverse_proxy chatwoot:3001
}

airbyte.{$DOMAIN} {
    reverse_proxy airbyte:8001
}

grafana.{$DOMAIN} {
    reverse_proxy grafana:3000
}

n8n.{$DOMAIN} {
    reverse_proxy n8n:5678
}
```

## Deploy Script

```bash
#!/usr/bin/env bash
set -euo pipefail

echo "=== AI Company — Deployment Script ==="

# Prerequisites
command -v docker >/dev/null 2>&1 || { echo "Requires Docker"; exit 1; }

# Validate .env
if [ ! -f .env ]; then
  echo "Missing .env — copy from .env.example"
  exit 1
fi
source .env

# Pull latest images
docker compose -f compose.core.yml pull
docker compose -f compose.apps.yml pull

# Deploy core infra first
echo "=== Deploying core infrastructure ==="
docker compose -f compose.core.yml up -d postgres minio

# Wait for postgres
echo "Waiting for PostgreSQL..."
until docker compose -f compose.core.yml exec -T postgres pg_isready -U postgres; do
  sleep 2
done

# Deploy remaining core
docker compose -f compose.core.yml up -d

# Deploy apps
echo "=== Deploying applications ==="
docker compose -f compose.apps.yml up -d

echo "=== Health check ==="
docker compose ps

echo "=== Deploy complete ==="
echo "Open WebUI:  https://{$DOMAIN}"
echo "Mattermost:  https://chat.{$DOMAIN}"
echo "Grafana:     https://grafana.{$DOMAIN}"
echo "n8n:         https://n8n.{$DOMAIN}"
echo "Keycloak:    https://auth.{$DOMAIN}"
echo "Support:     https://support.{$DOMAIN}"
```

## SSO Integration Map

| Service | Protocol | Keycloak Integration |
|---|---|---|
| Grafana | OIDC | `GF_AUTH_GENERIC_OAUTH_*` env vars |
| Open WebUI | OIDC | `WEBUI_AUTH_OPENID_PROVIDER_URL` |
| Mattermost | OIDC | System Console → Authentication → OpenID |
| n8n | OIDC | `N8N_AUTH_OIDC_*` env vars |
| Chatwoot | SAML | Enterprise tier only |
| Mautic | OIDC | Plugin required |
| Airbyte | OIDC | `AIRBYTE_AUTH_OIDC_*` env vars |
| MinIO | OIDC | `MINIO_IDENTITY_OPENID_CONFIG_URL` |
| Coolify | OIDC | Built-in SSO settings |

## Security Hardening Checklist

- [ ] Change all default passwords in `.env`
- [ ] Remove port mappings for internal services (use reverse proxy only)
- [ ] Configure firewall: allow only 80, 443, and SSH
- [ ] Enable Keycloak 2FA for admin user
- [ ] Set Grafana behind Keycloak SSO (disable `admin` local account)
- [ ] MinIO: enable TLS, set bucket policies to private
- [ ] PostgreSQL: set `password_encryption = scram-sha-256`
- [ ] PostgreSQL: configure `pg_hba.conf` to reject non-local connections
- [ ] Docker: enable content trust (`DOCKER_CONTENT_TRUST=1`)
- [ ] Docker: run `docker scan` on all images
- [ ] Fail2ban on SSH and Caddy
- [ ] Regular backups via Kopia (see Backup section)
