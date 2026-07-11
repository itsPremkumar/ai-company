# 🔧 Infrastructure, IAM & Observability Layer

**Role:** The production backbone — containers, deployment, secrets, identity, monitoring, messaging.
(Repos not re-verified in this session due to GitHub rate limits; use canonical paths.)

## Containers & Deployment
| Project | Link | Role |
|---|---|---|
| Docker | https://github.com/docker/docs | Containers |
| Kubernetes | https://github.com/kubernetes/kubernetes | Orchestration (scale later) |
| `coollabsio/coolify` | https://github.com/coollabsio/coolify (58.2k★, Apache-2.0) | Self-hostable PaaS |

## Identity & Secrets
| Project | Link | Role |
|---|---|---|
| `keycloak/keycloak` | https://github.com/keycloak/keycloak (35.6k★, Apache-2.0) | Auth/IAM |
| `Infisical/infisical` | https://github.com/Infisical/infisical (27.8k★) | Secrets mgmt |
| `hashicorp/vault` | https://github.com/hashicorp/vault | Secrets (enterprise) |

## Observability
| Project | Link | Role |
|---|---|---|
| `grafana/grafana` | https://github.com/grafana/grafana (75.5k★) | Dashboards |
| `prometheus/prometheus` | https://github.com/prometheus/prometheus | Metrics |
| `grafana/loki` | https://github.com/grafana/loki | Logs |
| `open-telemetry/opentelemetry` | https://github.com/open-telemetry/opentelemetry | Tracing |

## Storage & Messaging
| Project | Link | Role |
|---|---|---|
| `minio/minio` | https://github.com/minio/minio (61.3k★, AGPL-3.0) | S3 object storage |
| `postgres/postgres` | https://github.com/postgres/postgres | Database |
| `rabbitmq/rabbitmq` | https://github.com/rabbitmq/rabbitmq | Messaging |
| `nats-io/nats-server` | https://github.com/nats-io/nats-server | Event bus |
| `ntfy-org/ntfy` | https://github.com/ntfy-org/ntfy | Notifications |
| `centrifugal/centrifugo` | https://github.com/centrifugal/centrifugo (10.4k★, Apache-2.0) | Self-hosted real-time WebSocket/pubsub (Pusher alt) |

## Security
| Project | Link | Role |
|---|---|---|
| `wazuh/wazuh` | https://github.com/wazuh/wazuh | SOC/SIEM |
| `keycloak/keycloak` | (above) | IAM |

## Backup & Disaster Recovery
| Project | Link | Role |
|---|---|---|
| `kopia/kopia` | https://github.com/kopia/kopia (13.3k★, Apache-2.0) | Encrypted, deduplicated backups with web UI |

## API Gateway
| Project | Link | Role |
|---|---|---|
| `Kong/kong` | https://github.com/Kong/kong | API gateway |
| `openziti/ziti` | https://github.com/openziti/ziti | Zero-trust networking |

## Why
This layer is what makes it *enterprise-grade* vs hobbyist. Keycloak (SSO), Infisical (secrets),
Coolify (deploy), Grafana+Prometheus+Loki (observability), MinIO (assets), PostgreSQL (data) — all
open, self-hostable, $0 license cost.
