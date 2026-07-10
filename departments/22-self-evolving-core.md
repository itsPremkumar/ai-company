# 🧬 Self-Evolving Core — The Brain That Improves Itself

**Role:** The company's central intelligence that **grows over time** — rewrites its own memory,
prompts, skills, and strategies based on outcomes. This is the most important layer for an
autonomous AI company. Orchestrators (CrewAI/claw-empire) only *route*; this layer *evolves*.

## The main post: Hermes (self-improving agent)
- **Hermes Agent** · https://github.com/NousResearch/hermes-agent
- Tagline: *"The agent that grows with you."* Persistent memory, **skill creation**,
  tool/self-modification. This is the only project in this stack purpose-built as a
  **self-improving agent** — it is the MAIN POST.

## Supporting evolution layers
| Layer | Project | ★ | License | What it adds | Link |
|---|---|---|---|---|---|
| Memory evolution | `mem0ai/mem0` | 60.5k ✅ | Apache-2.0 | Consolidates, forgets, updates memories over time | https://github.com/mem0ai/mem0 |
| Knowledge evolution | `getzep/graphiti` | 28.6k ✅ | Apache-2.0 | Temporal knowledge graph — facts update as world changes | https://github.com/getzep/graphiti |
| Autonomous expansion | `Viku-AI/agent-zero` | (canonical) | MIT | Spawns/modifies its own sub-agents & tools at runtime | https://github.com/Viku-AI/agent-zero |
| Research evolution | `SakanaAI/AI-Scientist` | (canonical) | Apache-2.0 | Autonomously runs research loops + writes results | https://github.com/SakanaAI/AI-Scientist |

## Why these (not the orchestrators)
- `claw-empire` / `CrewAI` / `LangGraph` = **orchestration** (route tasks) — they do NOT evolve.
- `markus` = gives agents **memory across sessions** — evolution-*enabling*, not evolution itself.
- `MetaGPT` = simulates a company, doesn't rewrite its own core.
- **Hermes + Mem0 + Graphiti + AgentZero** = the only combo here with real self-improvement.

## The architecture (4 layers)
```
LAYER 1  THE BRAIN (self-improving):
   Hermes  ← main post, grows via skills + memory
   + Mem0 (memory evolution) + Graphiti (knowledge evolution)

LAYER 2  AUTONOMY (spawns/modifies agents):
   AgentZero  ← creates/modifies its own sub-agents & tools

LAYER 3  ORCHESTRATION (routes work):
   claw-empire (CEO desk) + CrewAI (roles) + LangGraph (resilient flows)

LAYER 4  DOMAIN AGENTS:
   Agent-Reach (research), OpenHands (coding), your Video-Gen (product)...
```

## How Hermes exposes itself to be controlled
For orchestrators (Layer 3) to command Hermes, Hermes must be a **callable tool**:
- Run Hermes as an **MCP server** (your `Automated-Video-Generator` already does this pattern), or
- Expose Hermes via its **CLI/API** and let CrewAI/LangGraph call it as a tool.

## ⚠️ Reality check
True "self-evolving" (agent modifies its own source → verifies → redeploys) is still research-grade.
Hermes's skill/memory system is the **most practical open version today**. AgentZero is closest to
"spawns its own tools." Combine them — do not rely on one. Paperclip Maximus is a *concept only*,
not production (flagged earlier).

## Integration
Hermes (main) ← learns from every task via Mem0/Graphiti → AgentZero expands capacity when needed →
claw-empire/CrewAI route domain work → domain agents execute (Agent-Reach, OpenHands, Video-Gen).
