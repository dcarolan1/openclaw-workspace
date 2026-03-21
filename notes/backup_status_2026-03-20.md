# Backup Status — 2026-03-21

## What Is Now Protected (Git Remote)

**Repository:** https://github.com/dcarolan1/openclaw-workspace.git (PRIVATE)
**Branch:** main
**Push verified:** ✅ 2026-03-21 04:48 UTC

### Protected files include:
- MEMORY.md, SOUL.md, IDENTITY.md, USER.md, AGENTS.md
- HEARTBEAT.md, TOOLS.md
- All daily logs (memory/*.md)
- All notes (notes/*.md) — plans, audits, workflows, directives, policies
- All content (content/**) — emails, team messages, legal drafts
- Assessment materials (PDFs from Brad)
- .gitignore

### Security:
- GitHub Personal Access Token stored in ~/.git-credentials (600 permissions)
- Token NOT in git history or repo URL
- .gitignore excludes: credentials, secrets, tokens, env files

---

## What Is NOT Protected Yet

| Item | Location | Risk | Recommendation |
|------|----------|------|----------------|
| **OpenClaw config** | ~/.openclaw/openclaw.json | Contains API keys, bot token, auth token | Manual backup to encrypted USB or separate secure repo |
| **Ollama models** | /usr/share/ollama/ | 25GB of model data | Re-downloadable from Ollama — low risk, high time cost to restore |
| **Git credentials** | ~/.git-credentials | GitHub PAT | Recreatable — low risk |
| **OpenClaw session data** | ~/.openclaw/agents/ | Conversation history | Regeneratable — medium value |
| **Browser profile** | ~/snap/chromium/ | Cached audit data | Disposable — low value |
| **System config** | /etc/ssh/, /etc/ufw/, systemd units | Server configuration | Manual backup recommended |
| **LMS config** | /etc/squeezeboxserver/ | Music server settings | Low value — quick to reconfigure |
| **Dissertation PDF** | ~/.openclaw/media/inbound/ | David's original file | David has the original — low risk |

---

## Backup Procedure Going Forward

### Automatic (Aaron does this):
- `git push` after every significant commit or at end of work session
- Verify push succeeded
- Report any push failures in daily brief

### Manual (David does periodically):
- Back up ~/.openclaw/openclaw.json to encrypted USB or secure location
- Back up ~/.git-credentials if token changes
- Consider: whole-disk backup using rsync to external drive (weekly)

---

## Next Step Recommendations

1. **Set up automated push** — OpenClaw cron job or git hook to push after every commit (Aaron can configure)
2. **Back up openclaw.json** — David copies to encrypted USB this weekend
3. **Consider encrypted backup** for the full ~/.openclaw/ directory — rsync to an external drive
4. **Long-term:** off-site backup (encrypted, to a cloud location David controls) for disaster recovery beyond local disk failure
