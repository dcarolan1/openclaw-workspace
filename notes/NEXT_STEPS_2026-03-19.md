# Post-Rebuild Plan — 2026-03-19

## Steps

1. **Install jq**
   - `sudo apt install jq`
   - Needed for JSON processing in automation scripts
   - Status: ✅ Done — jq-1.7 installed 2026-03-19

2. **Install Ollama**
   - Status: ✅ Done — Ollama 0.18.2 installed 2026-03-19

3. **Model stack — FROZEN**
   - qwen3:8b — approved for fast local work (~6 tok/sec, 5.2GB)
   - qwen3:32b — approved for quality local work (~1.5 tok/sec, 20GB)
   - Claude Opus — primary for high-stakes reasoning (Anthropic API)
   - **No additional model installs without explicit David approval.**
   - Status: ✅ Done — evaluated, approved, frozen

4. **Verify local model integration**
   - Configure OpenClaw to route to Ollama as a provider
   - Test inference, latency, and reliability
   - Confirm fallback to Anthropic when needed
   - Status: Not started

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
