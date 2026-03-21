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

## Notes
- Estimates are based on session token metrics + pricing. Not exact.
- Actual billing is at console.anthropic.com → Settings → Billing → Usage
- Will update daily in the morning brief
