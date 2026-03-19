# Web Search Setup — 2026-03-19

## Configuration

- **Provider:** Brave Search API
- **Config path:** `tools.web.search` in openclaw.json
- **Settings:**
  - enabled: true
  - provider: brave
  - apiKey: (set, redacted)
- **Free tier:** 2,000 queries/month

## Test Results

| Query Type | Query | Time | Result |
|------------|-------|------|--------|
| Partner lookup | "Deeper Walk International ministry" | 832ms | ✅ Clean, relevant |
| General/business | "best coffee roasters wholesale US" | 750ms | ✅ Clean, relevant |
| Technical | "ollama model storage path linux" | 641ms | ✅ Clean, relevant |

All queries under 1 second. Results are relevant and well-structured.

## SearXNG Status

- Not configured as native provider (OpenClaw doesn't support SearXNG natively)
- Can query public SearXNG instances via web_fetch as manual fallback
- Local SearXNG install deferred — Brave is sufficient for current needs

## Operating Rules

1. **Brave is primary and only search engine**
2. If results are weak/empty → refine query, try again
3. If still unclear → escalate to Claude reasoning
4. Do NOT query both engines automatically
5. Do NOT spam queries — minimum queries, maximum signal
6. Do NOT search when local knowledge is sufficient
7. Search is input, not authority — interpret, compare, synthesize
8. Never pass raw search output to David
9. Do NOT use for internal decisions already known
10. Do NOT use for anything involving sensitive/private data (keep local)

## Hard Constraints

- No browser tools enabled
- No browser automation
- No external system exposure
- Search only

## Endpoints

- Brave Search API: https://api.search.brave.com/
- Web fetch (for manual SearXNG fallback): any public SearXNG instance

## Restart/Recovery

If search stops working:
1. Check config: `openclaw status`
2. Verify key in config: tools.web.search.apiKey
3. Restart gateway: `openclaw gateway restart`
4. Test: ask Aaron to run a web search
