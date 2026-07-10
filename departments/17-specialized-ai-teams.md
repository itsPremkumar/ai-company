# Specialized AI Teams (the "hands" — agent frameworks)

**Role:** The agent runtimes that power every department above. These ARE the AI employees.

## Core agent frameworks (verified)
| Framework | ★ | License | Best for | Link |
|---|---|---|---|---|
| **CrewAI** | 55.3k | MIT | Role-based company (CEO/CFO/CMO agents) | https://github.com/crewAIInc/crewAI |
| **OpenHands** | 80.3k | Open | Autonomous software engineering | https://github.com/OpenHands/OpenHands |
| **MetaGPT** | 69.3k | MIT | Whole "AI Software Company" in a box | https://github.com/FoundationAgents/MetaGPT |
| **Microsoft AutoGen** | 59.6k | CC-BY-4.0 | Multi-agent conversation / research | https://github.com/microsoft/autogen |
| **LangGraph** | 37k★ | MIT | Resilient production workflows | https://github.com/langchain-ai/langgraph |
| **OpenClaw ecosystem** | 212k★(Hermes) | MIT | Agent templates + runtime | https://github.com/NousResearch/hermes-agent |
| `GreenSheep01201/claw-empire` | 1.3k | Apache-2.0 | CEO Desk orchestration | https://github.com/GreenSheep01201/claw-empire |
| `swarmclawai/swarmclaw` | 610★ | — | Self-hosted multi-agent runtime | https://github.com/swarmclawai/swarmclaw |
| `mergisi/awesome-openclaw-agents` | 3.8k | — | 162 production agent templates | https://github.com/mergisi/awesome-openclaw-agents |
| `MervinPraison/PraisonAI` | 8.4k | — | "Hire a 24/7 AI Workforce" | https://github.com/MervinPraison/PraisonAI |
| `trycua/cua` | 19.5k | — | Computer-Use Agents (desktop ops) | https://github.com/trycua/cua |
| `nanobrowser/nanobrowser` | 13.4k | — | AI web automation | https://github.com/nanobrowser/nanobrowser |
| `browserable/browserable` | 1.2k | — | Browser automation for agents | https://github.com/browserable/browserable |
| `oomol-lab/open-connector` | 1.2k | — | 1000+ SaaS auth gateway | https://github.com/oomol-lab/open-connector |

## ⚠️ Paperclip Maximus
- A **concept** (recursively self-improving agent, "Paperclip Maximizer"), NOT a mature production
  repo. I found no canonical high-star implementation. Use only for R&D / Innovation Lab, never core ops.

## Recommended stack for THIS company
- **Roles/Org:** CrewAI (maps to your 60-dept chart)
- **Coding:** OpenHands + Hermes
- **Reliability:** LangGraph
- **Orchestration:** claw-empire / swarmclaw
- **Glue:** automatisch / n8n
