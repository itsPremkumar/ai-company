# Data Engineering / BI / Analytics

**Role:** Data pipelines (ETL), dashboards, reporting, user behavior analytics.

## Recommended projects
| Project | ★ | License | Link |
|---|---|---|---|
| `airbytehq/airbyte` | 21.5k | MIT | https://github.com/airbytehq/airbyte (ELT pipelines, 600+ connectors) |
| `dagster-io/dagster` | 14k | Apache-2.0 | https://github.com/dagster-io/dagster (asset-centric pipeline orchestration) |
| `great-expectations/great_expectations` | 11.6k | Apache-2.0 | https://github.com/great-expectations/great_expectations (data quality validation) |
| `datahub-project/datahub` | 14k | Apache-2.0 | https://github.com/datahub-project/datahub (metadata platform / data catalog) |
| `grafana/grafana` | 75.5k | — | https://github.com/grafana/grafana (dashboards) |
| `SigNoz/signoz` | 28.7k | — | https://github.com/SigNoz/signoz (analytics/observability) |
| `langfuse/langfuse` | 30.9k | — | https://github.com/langfuse/langfuse (AI/LLM analytics) |
| `baserow/baserow` | 5.3k | — | https://github.com/baserow/baserow (databases/automation) |

## Why
Airbyte = ELT pipelines with 600+ connectors. Dagster = asset-centric orchestrator (modern Airflow alt).
Great Expectations = data quality validation (unit tests for data). DataHub = metadata catalog / data
discovery (LinkedIn open-source). grafana = BI dashboards. SigNoz = product analytics. langfuse =
AI-agent analytics. baserow = data storage + automations. All open, self-hostable.

## Integration
AI Data Engineer builds pipelines via Airbyte → Dagster orchestrates → Great Expectations validates →
DataHub catalogs → BI agent builds grafana dashboards → CEO reviews KPIs.
