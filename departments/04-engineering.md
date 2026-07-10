# Engineering (Software / Web / Mobile / DevOps)

**Role:** Backend, frontend, APIs, web + mobile apps, system development, CI/CD, infra.

## Recommended projects
| Project | ★ | License | Link |
|---|---|---|---|
| `OpenHands/OpenHands` | 80.3k | Open | https://github.com/OpenHands/OpenHands (autonomous SWE) |
| `TabbyML/tabby` | 33.7k | Apache-2.0 | https://github.com/TabbyML/tabby (self-hosted Copilot) |
| `QwenLM/qwen-code` | 25.9k | Apache-2.0 | https://github.com/QwenLM/qwen-code (terminal AI coding agent) |
| `Danau5tin/multi-agent-coding-system` | 1.4k | — | https://github.com/Danau5tin/multi-agent-coding-system |
| `FoundationAgents/MetaGPT` | 69.3k | MIT | https://github.com/FoundationAgents/MetaGPT (AI software company) |
| `superplanehq/superplane` | 3.8k | — | https://github.com/superplanehq/superplane (dev control plane) |
| **Hermes (this agent)** | 212k★ | — | https://github.com/NousResearch/hermes-agent (coding engine) |
| `microsoft/autogen` | 59.6k | CC-BY-4.0 | https://github.com/microsoft/autogen |

## Why
OpenHands handles autonomous SWE; Tabby provides self-hosted Copilot-style code completion; Qwen Code
is a lightweight terminal-first coding agent for quick edits. MetaGPT builds whole software from a
one-line req. Hermes handles targeted coding/deploy. Together they cover every coding scenario.

## Integration
CTO agent splits work → OpenHands/Hermes implement → `superplane` tracks → tests run in CI.
