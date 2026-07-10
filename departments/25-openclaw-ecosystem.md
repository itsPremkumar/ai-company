# 🐾 OpenClaw — Full Ecosystem Breakdown (verified)

> Researched live from openclaw.ai, github.com/openclaw, and clawhub.ai.
> OpenClaw is the **open-source personal AI assistant** ecosystem — relevant to your AI company as
> both an orchestration runtime AND a source of agent "skills" (reusable capabilities).

## 🏠 Core
| Project | ★ | Lang | Link | Role |
|---|---|---|---|---|
| **`openclaw/openclaw`** | **382.5k** | — | https://github.com/openclaw/openclaw | The main assistant — "Your own personal AI assistant. Any OS. Any Platform." |
| `openclaw/clawhub` | 9.1k | TypeScript | https://github.com/openclaw/clawhub · https://clawhub.ai | **Skill + Plugin Registry** (the app store for Claws) |

## 🌐 Official site & docs
- Website: https://openclaw.ai/
- Docs: https://docs.openclaw.ai/
- ClawHub marketplace: https://clawhub.ai/
- Discord / GitHub linked from site

## 🧩 ClawHub — the Skill & Plugin Registry (clawhub.ai)
ClawHub is the **marketplace** where agents install "skills" (capabilities) and "plugins."
Trending skills (live from clawhub.ai):
| Skill | Creator | What it does |
|---|---|---|
| self-improving agent | @pskoett | Captures learnings/errors/corrections → continuous improvement |
| Skill Vetter | @spclaudehome | Security-first vetting before installing any skill |
| Self-Improving + Proactive Agent | @ivangdavila | Self-reflection + self-criticism + self-learning memory |
| Github | @steipete | `gh` CLI — issues, PRs, runs |
| ontology | @oswalpalash | Typed knowledge graph for structured agent memory |
| Gog | @steipete | Google Workspace CLI (Gmail/Calendar/Drive/Docs) |
| SkillScan | @tokauthai | Security gate — every new skill MUST pass before use |
| Proactive Agent | @halthelobster | Transforms agents from task-followers to proactive partners |
| Weather | @steipete | Weather/forecasts, no API key |

**Key insight:** ClawHub's most popular skills are **self-improving / memory / security-vetting** —
exactly the capabilities your `22-self-evolving-core.md` needs. OpenClaw + ClawHub is a
**ready-made skill marketplace** you can plug into Hermes.

## 🛠 The OpenClaw org — full project list (verified)
| Repo | ★ | Role |
|---|---|---|
| `openclaw/openclaw` | 382.5k | Main assistant |
| `openclaw/clawhub` | 9.1k | Skill/plugin registry |
| `openclaw/agent-skills` | 875 | Useful skills for agents & claws |
| `openclaw/clawpatch` | 770 | Review code, patch bugs, land PRs |
| `openclaw/crabfleet` | 212 | Mission control for agent runs |
| `openclaw/clickclack` | 168 | Chat app with claws |
| `openclaw/clawpdf` | 96 | Zero-dep PDFium WASM bindings |
| `openclaw/octopool` | 95 | Org-authenticated GitHub read relay |
| `openclaw/libopus-wasm` | 91 | WASM libopus bindings |
| `openclaw/telecrawl` | 66 | Telegram for Claws |
| `openclaw/clawrouter` | 34 | API gateway + provider router |
| `openclaw/rastermill` | 35 | Image processing for Node agents |
| `openclaw/crawlkit` | 51 | Go infra for local-first crawlers |
| `openclaw/clawscan` | 8 | Security scanning harness for skills |
| `openclaw/crabhelm` | 2 | Meta Orchestrator |
| `openclaw/turnwire` | 11 | Audited text-only MCP relay |
| `openclaw/ffmpeg-wasm` | 47 | FFmpeg/FFprobe for Node |
| `openclaw/design-system` | 3 | Web design tokens/GUI |
| `openclaw/rfcs` | 9 | RFCs |
| `openclaw/ask-molty` | 25 | Docs builder |

## 🔗 How it fits YOUR ai-company stack
1. **As orchestration runtime:** OpenClaw (`openclaw/openclaw`) can be the agent runtime; ClawHub
   supplies skills (self-improving, memory, GitHub, Gog) — complements `claw-empire` / CrewAI.
2. **As skill source:** Install ClawHub's *self-improving* + *memory (ontology)* + *SkillScan
   (security)* skills into Hermes → directly upgrades your `22-self-evolving-core.md` brain.
3. **As product:** You could publish your own `Automated-Video-Generator` MCP as a ClawHub skill →
   distribution channel + community (ties to OSPO in `24-additional-departments.md`).

## ⚠️ Notes
- OpenClaw is **huge** (382k★) and fast-moving; some org repos are tiny/experimental (crabhelm 2★,
  uirouter 2★) — treat those cautiously (same rule as Paperclip: check maintenance before prod).
- ClawHub skills are community-contributed — **always vet via SkillScan/Skill Vetter before install**
  (security).
- Licenses vary across org repos — check per-repo before bundling into your company.

## Related (outside the org, OpenClaw-adjacent)
- `NousResearch/hermes-agent` (212k★) — Hermes, your main agent (listed as OpenClaw-adjacent in
  searches; "grows with you" = same self-improving philosophy)
- `nanocoai/nanoclaw` (30k★) — lightweight OpenClaw alternative in containers
- `zeroclaw-labs/zeroclaw` (32k★) — fast autonomous personal assistant
- `garrytan/gbrain` (25.8k★) — "Opinionated OpenClaw/Hermes Agent Brain"
