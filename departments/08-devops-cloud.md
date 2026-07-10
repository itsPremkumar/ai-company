# DevOps / Cloud / SRE / Security / Network / DBA

**Role:** CI/CD, deployment, cloud infra, reliability, security, networking, databases.

## Recommended projects
| Project | ★ | License | Link |
|---|---|---|---|
| `superplanehq/superplane` | 3.8k | — | https://github.com/superplanehq/superplane (dev control plane) |
| `grafana/grafana` | 75.5k | — | https://github.com/grafana/grafana (observability) |
| `SigNoz/signoz` | 28.7k | — | https://github.com/SigNoz/signoz (SRE/observability) |
| `langfuse/langfuse` | 30.9k | — | https://github.com/langfuse/langfuse (LLM/AI security observability) |
| `certimate-go/certimate` | 8.8k | — | https://github.com/certimate-go/certimate (SSL/keys mgmt) |
| Wazuh | — | GPL | https://github.com/wazuh/wazuh (open SOC/SIEM) |
| `bytechefhq/bytechef` | 903★ | — | https://github.com/bytechefhq/bytechef (agent orchestration + workflows) |

## Why
grafana + SigNoz = full SRE observability. langfuse watches AI-agent behavior (security). certimate
manages TLS. Wazuh = open SOC. All self-hostable, $0.

## Integration
AI DevOps/SRE agents monitor via grafana/SigNoz → alert on incidents → AI SecOps reviews via langfuse/Wazuh.
