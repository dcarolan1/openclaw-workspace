# AI Cost Tracking — Daily Log

## Pricing Reference
| Model | Input (uncached) | Input (cached) | Output |
|-------|-----------------|----------------|--------|
| Claude Opus 4 | $15/MTok | $1.875/MTok | $75/MTok |
| qwen3:8b (local) | Free | Free | Free |
| qwen3:32b (local) | Free | Free | Free |

## Cost Reduction Strategy
- Use qwen3:32b for first drafts, Claude for refinement only
- Keep sessions alive longer (reduce compactions = more cache hits)
- Batch related work in single sessions
- Short confirmations (NO_REPLY when appropriate) save output tokens

---

## Daily Log

### March 19, 2026
- First boot + full rebuild
- Identity restore, system audit, Ollama install, model evals
- Heavy session — multiple compactions
- **Est. cost: $60-80**

### March 20, 2026
- Dissertation ingestion (large PDF), assessment audit (4 PDFs)
- 8 emails written + multiple rewrites
- Formation upgrade, voice profile, master directive
- Brad/Theresa email, security review, GitHub backup
- Very heavy day — longest sessions, most output
- **Est. cost: $100-130**

### March 21, 2026 (so far)
- Command brief, inbox triage, 2 emails sent (Theresa research, Brad reconnect)
- 7 partner outreach emails drafted
- Security hardening, UFW, DHCP troubleshooting
- Email access restored (Graph API)
- **Est. cost so far: $30-40**

---

### Running Total
| Period | Estimated Cost |
|--------|---------------|
| Mar 19 | $60-80 |
| Mar 20 | $100-130 |
| Mar 21 (partial) | $30-40 |
| **Total (3 days)** | **$190-250** |

_David reported ~$200 spent on Anthropic, which aligns with this estimate._

---

## Pending: Multi-Model Routing (Connect When Ready)

**David has API keys for:**
- Grok (xAI) — used for assessment design, creative work
- ChatGPT / GPT-4o (OpenAI) — general purpose, cheaper than Opus

**Connect when these conditions are met:**
1. JR April 15 relaunch is executing (not planning)
2. Brad and Theresa are actively working on tasks
3. Aaron has bandwidth for system integration work
4. A natural pause in execution (not mid-deliverable)

**What Aaron will do with them:**
- Route first drafts → GPT-4o (80% cheaper than Opus)
- Route research synthesis → Grok or GPT-4o
- Route quick lookups → qwen3:8b (free)
- Keep final quality / David-facing → Opus only

**Expected impact:** 30-50% reduction in Anthropic monthly costs

**Aaron will prompt David when ready:**
> "David — we have bandwidth to connect GPT-4o and Grok APIs. This will reduce our Anthropic costs by routing drafts and research through cheaper models. Can you provide the API keys?"

## Notes
- Estimates are based on session token metrics + pricing. Not exact.
- Actual billing is at console.anthropic.com → Settings → Billing → Usage
- Will update daily in the morning brief
