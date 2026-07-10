# Telecalling / Call Center / Voice AI

**Role:** Inbound/outbound calls, AI voice assistant, telecalling.

## Recommended projects
| Project | ★ | License | Link |
|---|---|---|---|
| `dograh-hq/dograh` | 4.8k | BSD-2-Clause | https://github.com/dograh-hq/dograh (Vapi alt, self-hosted voice AI) |
| `PatterAI/Patter` | 953★ | — | https://github.com/PatterAI/Patter (voice-AI SDK) |
| `devnen/Chatterbox-TTS-Server` | 1.3k | — | https://github.com/devnen/Chatterbox-TTS-Server (self-host TTS) |
| `kirklandsig/AIReceptionist` | 57★ | — | https://github.com/kirklandsig/AIReceptionist (AI phone receptionist) |
| `mohitbadwal/ringback` | 16★ | — | https://github.com/mohitbadwal/ringback (MCP: AI calls your phone) |
| FreeSWITCH / Asterisk | — | open | PBX backbone for scale |

## Why
**dograh** is the key tool — open self-hosted voice AI platform (Vapi/Retell alternative), handles
inbound/outbound calls. Chatterbox-TTS for voice synthesis. ringback lets the AI agent call YOU.
FreeSWITCH/Asterisk = open PBX for volume.

## Integration
AI Telecaller (dograh) → outbound lead calls → logs to NocoBase CRM → escalates to human via ringback.
