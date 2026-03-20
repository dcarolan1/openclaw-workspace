# Browser Usage Policy — 2026-03-19

## Configuration
- **Browser:** Chromium 146.0.7680.80 (snap)
- **Mode:** Headless (no display)
- **Sandbox:** Disabled (required for snap Chromium)
- **Executable:** /usr/bin/chromium-browser
- **Profile data:** Symlinked to snap-accessible path (~/snap/chromium/common/openclaw-browser)

## Rules

### Allowed Uses
- Explicit task-based site audits (e.g., JR assessment flow)
- Form interaction and testing (e.g., taking an assessment)
- Page structure analysis that web_fetch can't capture (JavaScript-rendered content, images, interactive elements)
- Verifying user experience flows end-to-end

### Prohibited Uses
- No autonomous browsing — browser only opens when David instructs or a task explicitly requires it
- No wandering or exploratory searching
- No browser-based web search (use Brave API for search)
- No logging into David's personal accounts without explicit permission
- No browser automation beyond the immediate task
- No persistent sessions — close tabs when done

### Output Rules
- All browser findings must be written to disk
- Screenshots saved to workspace when relevant
- Never pass raw browser output to David — synthesize and summarize

### Hard Constraints
- Browser is a task tool, not an always-on capability
- Close browser sessions after each task
- If a task can be done with web_fetch, prefer web_fetch (lighter, faster, no browser overhead)
- Browser does NOT replace web search — it supplements it for interactive/visual tasks only

## Recovery
If browser fails to start:
1. Kill stale Chromium: `pkill -f chromium`
2. Remove singleton lock: `rm -f /home/aaron/snap/chromium/common/openclaw-browser/SingletonLock`
3. Retry
