# Post-Rebuild Plan — 2026-03-19

## Steps

1. **Install jq**
   - `sudo apt install jq`
   - Needed for JSON processing in automation scripts
   - Status: Pending (needs sudo)

2. **Install Ollama**
   - Install runtime and verify GPU/CPU support
   - Status: Not started

3. **Recommend model set**
   - Evaluate local models for David's use cases: coding, writing, research, business ops
   - Balance quality vs. resource usage (62GB RAM available)
   - Deliver recommendation with rationale
   - Status: Not started

4. **Verify local model integration**
   - Configure OpenClaw to route to Ollama as a provider
   - Test inference, latency, and reliability
   - Confirm fallback to Anthropic when needed
   - Status: Blocked on #2/#3

5. **Define active workflows**
   - Map David's day-to-day needs across businesses (GJ, BAG, E456, JR, KNGD VNTRS, Rhythm.Coffee)
   - Build workflows using current tools only (Telegram, CLI, OpenClaw cron, supported integrations)
   - No Mission Control. No legacy tooling.
   - Status: Not started

6. **Define backup strategy**
   - Workspace git commits (local)
   - Remote git push (needs remote configured)
   - Config backup approach
   - Memory/notes protection
   - Status: Not started
