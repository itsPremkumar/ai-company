# QA / Test Automation / Technical Writing / Knowledge Mgmt

**Role:** Manual + automated testing, documentation, internal knowledge base.

## Recommended projects
| Project | ★ | License | Link |
|---|---|---|---|
| **Hermes (this agent)** | 212k★ | — | https://github.com/NousResearch/hermes-agent (runs test suites) |
| `OpenHands/OpenHands` | 80.3k | Open | https://github.com/OpenHands/OpenHands (auto bug fixes) |
| `langfuse/langfuse` | 30.9k | — | https://github.com/langfuse/langfuse (LLM evals) |
| `usebruno/bruno` | 45.4k | MIT | https://github.com/usebruno/bruno (open-source Postman alt, git-native API client) |
| `grafana/k6` | — | AGPL-3.0 | https://github.com/grafana/k6 (load testing — JavaScript, CI/CD-native) |
| `baserow/baserow` | 5.3k | — | https://github.com/baserow/baserow (knowledge base) |
| `eclaire-labs/eclaire` | 883★ | — | https://github.com/eclaire-labs/eclaire (local AI assistant/docs) |

## Why
QA = Hermes runs the project's test suites (verified: 57/57 on your video project). OpenHands auto-fixes
bugs. langfuse evaluates AI output. Bruno is the git-native API client for manual + automated API testing.
k6 runs load tests in CI/CD. baserow/eclaire manage docs.

## Integration
AI QA agent runs tests via Hermes → Bruno for API testing → k6 for load/performance → langfuse tracks
AI quality → reports failures to Engineering.
