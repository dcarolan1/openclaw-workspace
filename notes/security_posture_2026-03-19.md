# Security Posture Review — 2026-03-21

**System:** openclaw-box (Intel i7-10700T, Ubuntu 24.04)
**Auditor:** Aaron Aidel
**Approach:** Honest assessment. Nothing assumed secure unless verified.

---

## 1. What Is Currently Protected

### Firewall (UFW)
- **Active** with default DROP policy on INPUT
- SSH (22/tcp) allowed
- LMS ports (9000, 9090, 3483) allowed
- All local subnet (192.168.0.0/24) allowed (broad — see risks)
- **Status: GOOD** — external inbound is blocked by default

### SSH
- **Password authentication disabled** — key-only access ✅
- Listening on all interfaces (0.0.0.0 and ::) — standard for a server
- **fail2ban is active** ✅
- Only two shell users: root and aaron
- **Status: GOOD** — key-only + fail2ban is solid

### Telegram Channel
- **allowFrom restricted** to David's Telegram ID (1558675102) only
- DM policy: pairing (explicit approval required)
- Group policy: allowlist
- Bot token stored in openclaw.json (600 permissions, aaron-only) ✅
- **Status: GOOD** — tight access control

### OpenClaw Gateway
- Listening on **localhost only** (127.0.0.1:18789, 18791, 18792)
- **Not exposed to network** ✅
- Auth: token-based
- **Status: GOOD**

### Ollama
- Listening on **localhost only** (127.0.0.1:11434)
- **Not exposed to network** ✅
- **Status: GOOD**

### OpenClaw Config File
- Permissions: **-rw------- (600)** — aaron-only read/write ✅
- Contains: Anthropic API key, Brave API key, Telegram bot token, gateway auth token
- **Status: GOOD** — proper permissions

### Model Stack
- Frozen. qwen3:8b + qwen3:32b + Claude Opus. No changes without David's approval.
- **Status: GOOD**

### Automatic Security Updates
- **unattended-upgrades is active** ✅
- OS patches applied automatically
- **Status: GOOD**

---

## 2. What Is Still At Risk

### 🔴 HIGH RISK

**No git remote / no off-box backups**
- All workspace data exists on ONE disk only
- No remote git repository configured
- No automated backup to external storage
- A disk failure, accidental deletion, or compromise = total loss
- **Impact: CRITICAL** — everything we've built (plans, emails, audits, memory) has no backup

**LMS exposed on all interfaces (0.0.0.0:9000, 9090, 3483)**
- Anyone on the local network can access the LMS web UI
- No authentication on LMS by default
- Port 9000 was opened in UFW for local network access (Squeezer)
- **Impact: LOW** (local network only) but sloppy — should be restricted to specific IPs

**Chromium running persistently with --no-sandbox**
- Browser is headless but running with reduced security isolation
- Snap confinement provides some protection, but no-sandbox weakens it
- Running continuously since last browser session — should be stopped when not in use
- **Impact: MEDIUM** — potential attack surface if a malicious page is loaded

**Broad UFW rule: allow from 192.168.0.0/24**
- Added to fix Squeezer connectivity
- Opens ALL ports to every device on the local network
- Any compromised IoT device on the network could reach any service on this box
- **Impact: MEDIUM** — should be tightened to specific IPs and ports

### 🟡 MEDIUM RISK

**Secrets in config file (not encrypted at rest)**
- Anthropic API key, Brave API key, Telegram bot token, gateway token all in plaintext in openclaw.json
- File permissions are correct (600) but no disk encryption detected
- If someone gains physical access to the machine or the disk, all secrets are readable
- **Impact: MEDIUM** — physical access risk

**Browser profile data stored unencrypted**
- Chromium profile at ~/snap/chromium/common/openclaw-browser/
- Could contain cached pages, cookies, browsing history from audit sessions
- **Impact: LOW-MEDIUM** — contains JR site data from audit

**No disk encryption**
- LVM volume (ubuntu--vg-ubuntu--lv) is **not** LUKS-encrypted
- Physical disk theft = full data access
- **Impact: MEDIUM** — physical access scenario

**Email credentials (pending)**
- MS 365 Graph API credentials will be stored on this box
- Need to ensure they're stored with proper permissions (600, not in git)
- **Impact: MEDIUM** — not yet active, but plan ahead

### 🟢 LOW RISK

**CUPS printing service listening (port 631)**
- CUPS is listening on all interfaces
- Unlikely attack vector but unnecessary exposure
- **Impact: LOW** — disable if printing isn't needed

**Two users with bash shells (root + aaron)**
- Root has a shell but likely no password set (Ubuntu default)
- Aaron is the only active user
- **Impact: LOW** — normal configuration

**No system crontab utility**
- crontab command not installed (OpenClaw uses its own cron)
- Not a risk per se, but means system-level scheduled tasks can't be set easily
- **Impact: LOW**

---

## 3. Immediate Hardening Actions (Highest Priority Only)

### Action 1: Set up off-box backup (CRITICAL)

**What:** Configure a git remote and push workspace to it. Also back up openclaw.json.

**Options:**
- Private GitHub/GitLab repo (free, encrypted in transit)
- USB drive backup (manual, but better than nothing)
- rsync to another machine on the network

**Effort:** 10 minutes for git remote. David needs to create the repo.

**Why now:** One disk failure and we lose everything from the past 3 days. Unacceptable.

### Action 2: Tighten UFW rules

**What:** Replace `allow from 192.168.0.0/24` with specific rules:
```
sudo ufw delete allow from 192.168.0.0/24
sudo ufw allow from 192.168.0.187 to any port 9000,9090,3483 proto tcp
sudo ufw allow from 192.168.0.189 to any port 9000,9090,3483 proto tcp
```
(Replace with David's actual device IPs — phone + laptop)

**Effort:** 5 minutes. Needs sudo.

**Why now:** The broad rule is a lazy shortcut from the LMS setup. Fix it.

### Action 3: Stop Chromium when not in use

**What:** Close browser sessions after each audit task. Don't leave Chromium running 24/7.

**Implementation:** Aaron already has this as a policy in browser_policy_2026-03-19.md. Enforce it now — Chromium is currently running from last night's session.

**Effort:** Immediate.

```
pkill -f chromium
```

### Action 4: Store email credentials securely

**What:** When MS 365 Graph API creds are restored, store them in `~/.openclaw/credentials/` (already exists, 700 permissions) — NOT in the workspace, NOT in git.

**Effort:** 5 minutes when creds are provided.

---

## 4. Approval Matrix

### Aaron May Take Autonomously
- Close browser sessions after use
- Monitor logs for suspicious activity
- Rotate non-critical tokens (if supported)
- Update workspace file permissions
- Add .gitignore rules to protect secrets
- Report security concerns to David via Telegram
- Run system status checks
- Commit and push to git remote (once configured)

### Requires David's Approval
- Any UFW / firewall rule changes
- Adding or removing SSH keys
- Installing new software or services
- Opening new network ports
- Storing new credentials
- Granting access to any external party
- Changes to OpenClaw config (gateway, channels, auth)
- Disk encryption or major system changes
- Backup strategy decisions (where, how, frequency)

### Permanently Prohibited
- Exposing any service to the public internet
- Disabling UFW or fail2ban
- Sharing credentials, API keys, or tokens externally
- Granting anyone (including Brad, Theresa, or other team members) direct access to openclaw-box
- Installing remote access tools beyond SSH
- Running services as root
- Storing secrets in the git workspace
- Modifying SSH configuration
- Accessing David's personal accounts without explicit instruction

---

## Summary

| Area | Status |
|------|--------|
| Firewall | ✅ Active, needs tightening |
| SSH | ✅ Key-only + fail2ban |
| Telegram | ✅ Restricted to David |
| Gateway | ✅ Localhost only |
| Ollama | ✅ Localhost only |
| Config permissions | ✅ 600, aaron-only |
| Auto-updates | ✅ Active |
| **Backups** | **❌ CRITICAL GAP — no off-box backup** |
| LMS exposure | ⚠️ All interfaces, no auth |
| Browser | ⚠️ Running with no-sandbox, should be stopped |
| UFW broad rule | ⚠️ Needs tightening |
| Disk encryption | ⚠️ Not encrypted |

**Bottom line:** The system is reasonably secure for a local box behind a home router. SSH is solid, services are mostly localhost-only, config permissions are correct. **The one critical gap is backups.** Everything else is medium-priority hardening. Fix the backup, tighten UFW, stop leaving Chromium running, and this box is in good shape.
