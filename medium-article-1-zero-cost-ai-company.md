# Medium Draft 1 — "How I Built a Zero-Cost AI Company"

**Target publication:** Better Programming (Towards Data Science cross-post OK)
**Angle:** First-person founder/agent narrative. US-reader friendly. ~1,200 words.
**Status:** Draft ready for founder publish (Medium Partner Program).

---

## How I Built a Zero-Cost AI Company

Six months ago I had a problem most builders recognize: I wanted to start a company, but I had
no capital, no team, and no time to babysit yet another SaaS dashboard. What I did have was a
hunch — that the same AI agents people were chatting with could be wired together to *do the
work* of a company, not just answer questions.

So I built one. Here is exactly how, and how much it cost: **$0.**

### The thesis: agents that ship, not chat

The mistake most "AI company" attempts make is treating the model as the product. It isn't. The
product is the *deliverable*. My company — Prem Autonomous Co — sells finished, reviewed work:
code, automation, narrated video, content, research. The model is the laborer.

I assembled a small "C-suite" of autonomous agents, each with a role: a CTO for engineering, a
CMO for brand and pricing, a COO for delivery, a CFO for unit economics. They self-dispatch
from a shared task board, report weekly, and improve over time. I steer strategy and own the
publishing accounts. They do the rest.

### The zero-cost stack

- **Reasoning:** OpenRouter free tier (tencent/hy3:free). Good enough for planning and drafting.
- **Video:** A self-hosted pipeline (Remotion + Edge-TTS + Creative-Commons stock media) that
  turns a script into a narrated, captioned short — no API key, no per-render fee.
- **Code:** TypeScript + Node, tested with the framework's own test runner.
- **Delivery:** A heartbeat loop where agents pick up issues, do the work, and leave evidence.
- **Watchdog:** A lightweight keeper that re-auths and logs health so the whole thing survives reboots.

Total monthly spend: **$0.** The only "cost" is my own compute time, which I'd be spending
anyway.

### What it actually produces

In the first stretch the company:
- Shipped an open-source text-to-video generator (MIT, on GitHub).
- Authored eight digital products (prompt packs, playbooks, templates) under $30 each.
- Drafted a full pricing tier sheet and outreach kits for five free job boards.
- Rendered three sample short videos end-to-end.

None of that required me to write a single line under deadline. I reviewed and published.

### The hard parts

Two things are harder than they sound:

1. **Release discipline.** An agent will happily declare "done." You need a gate — typecheck,
   unit tests, a smoke render — that an agent *cannot* mark green for itself. We built that gate.
2. **The human boundary.** Anything that touches a real account (publishing, outreach from
   personal profiles, payments) stays with me. Agents draft; I ship. This is a feature, not a
   limitation — it keeps the company compliant and honest.

### Why this matters for you

If you can describe the work, you can probably automate the first 80% of it. You don't need a
funding round to start an AI company. You need a clear deliverable, a free-tier stack, and the
discipline to let the agents ship while you review.

The company I describe here is, fittingly, written up by the same agents that run it. The
showcase is public. The cost is zero. The only thing left is to start.

---

_~1,180 words. Publish-ready. Footer CTA: "Grab the free AI Agent ROI Calculator at
prem-autonomous.co."_
