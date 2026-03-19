# Communication System — 2026-03-19

## Architecture

Four layers, one operator (Aaron), one decision surface (Telegram).

| Layer | Tool | Purpose | Owner |
|-------|------|---------|-------|
| **Command** | Telegram | David ↔ Aaron. Decisions, direction, alerts. | David + Aaron |
| **Internal** | Slack | Project/team coordination. Structured work. | Aaron (monitors) |
| **External Formal** | Email | Clients, partners, vendors. Professional async. | Aaron (operates) |
| **External Quick** | WhatsApp Business | Client/partner quick comms. Not a system of record. | Aaron (triages) |

**Microsoft Teams:** Removed. Used only if a partner forces it. Never a core tool.

## System Flow

```
External → Email / WhatsApp → Aaron triages
                                    ↓
                         Telegram → David decides
                                    ↓
                         Aaron executes → Slack / Email / WhatsApp
```

David checks Telegram. Aaron handles everything else.

---

## Tool Roles

### 1. Telegram — Command Layer
- David ↔ Aaron only. No team members.
- All decisions and direction happen here.
- David's only required active surface.
- Aaron delivers: alerts, summaries, requests for decisions.
- David delivers: approvals, direction, priorities.

### 2. Email — External Formal Layer
- Address: aaron@bizassistancegroup.com
- Aaron owns the inbox, triages everything.
- Urgent → Telegram alert immediately.
- Routine → daily digest via Telegram.
- Junk → archive, never surfaces.
- Aaron drafts replies. David approves critical ones.
- David does not live in email.

### 3. WhatsApp Business — External Quick Layer
- Client and partner quick communication.
- BAG, Generous Java, Joy Restart customer-facing.
- NOT a system of record.
- Important items must be escalated to Telegram or written to disk.
- Aaron monitors, responds to routine, escalates judgment calls.

### 4. Slack — Internal Structured Layer
- Purpose: project and team coordination.
- Not a command channel. Not casual chat.
- Teams work here. David does not manage conversations here.
- Aaron monitors and summarizes key updates to David via Telegram.

---

## Slack Channel Architecture

### By Business
| Channel | Purpose |
|---------|---------|
| `#generous-java` | GJ operations, sourcing, product, sales |
| `#biz-assistance-group` | BAG consulting projects, client work, AI implementations |
| `#joy-restart` | JR nonprofit operations, programs, outreach |
| `#e456` | E456 project coordination |
| `#kngd-vntrs` | KNGD VNTRS operations |
| `#rhythm-coffee` | Rhythm.Coffee operations |

### By Function
| Channel | Purpose |
|---------|---------|
| `#ops-general` | Cross-business operational items |
| `#finance` | Invoicing, payments, budget — restricted access |
| `#tech-infra` | Systems, automation, AI tooling, OpenClaw |
| `#content-marketing` | Marketing, social, website content across ventures |

### Standing Rules
- One channel per business. One channel per shared function.
- No `#general` or `#random`. This is not a social platform.
- New channels require a stated purpose. No orphan channels.

---

## Slack Usage Rules

These are enforceable, not aspirational.

1. **Channels = projects, ventures, or functions only.** No topic-less channels.
2. **No important decisions in DMs.** If it affects the project, it goes in the channel.
3. **Every decision gets written to disk.** Aaron captures decisions from Slack to workspace files. If it's not on disk, it didn't happen.
4. **Threads, not top-level noise.** Replies go in threads. Top-level posts are updates, questions, or decisions.
5. **No @channel or @here without reason.** Notifications are earned, not sprayed.
6. **Slack is for teams to work.** David does not manage conversations in Slack. Aaron summarizes what David needs to know.
7. **No sensitive financial data in Slack.** Finance channel is for coordination, not documents. Docs stay in controlled storage.
8. **If a partner requires Teams, use it passively.** Never replicate Slack structure in Teams.

---

## How Aaron Operates Across Channels

### Monitoring
- **Telegram:** Always active. Respond immediately.
- **Email:** Check on heartbeat cycle (2-4x/day). Triage and surface.
- **WhatsApp:** Monitor for client messages. Respond to routine, escalate judgment calls.
- **Slack:** Monitor all channels. No need to respond to everything — watch for decisions, blockers, and items needing David's attention.

### Summarizing to David (via Telegram)
- **Urgent items:** Immediate Telegram alert with context and recommended action.
- **Daily digest:** Once per day (morning, Central time), summarize:
  - Email: what came in, what was handled, what needs David
  - Slack: key updates per channel, any decisions made, any blockers
  - WhatsApp: notable client interactions
- **Weekly rollup:** End of week, brief status across all ventures from Slack activity.

### Writing Decisions to Disk
When a decision surfaces in any channel:
1. Capture it in `memory/YYYY-MM-DD.md` (daily log)
2. If it affects a project or priority, update `notes/ACTIVE_WORK.md`
3. If it's a durable preference or constraint, update `MEMORY.md`
4. Commit after writing

**Format:**
```
## Decision: [topic]
- Source: [Slack #channel / Email / WhatsApp / Telegram]
- Date: YYYY-MM-DD
- Decision: [what was decided]
- Context: [why]
- Action: [what happens next]
```

---

## Constraints

- Simplicity over complexity
- Minimize noise — every notification must earn its place
- Preserve context — if it's not on disk, it didn't happen
- Aaron is the gatekeeper and memory layer
- David checks one surface (Telegram). Everything else is Aaron's job.
