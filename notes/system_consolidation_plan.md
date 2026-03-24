# System Consolidation + Operational Upgrade — Phase 1

**Date:** 2026-03-24
**Status:** ACTIVE — executing step by step
**Principle:** M365 = single operating system. Aaron = central operator. Telegram = decision surface.

---

## Status Tracker

| # | Task | Status | Blocker |
|---|------|--------|---------|
| 1 | Proton → M365 forwarding (JR) | NOT STARTED | Need Proton admin access |
| 2 | Create/verify JR mailbox in M365 | NOT STARTED | Need M365 admin access |
| 3 | Shared mailboxes (support@jr, partners@jr, hello@gj, orders@gj) | NOT STARTED | Need M365 admin + DNS |
| 4 | Brad: SMTP → M365, form validation, WooCommerce flows | NOT STARTED | Depends on #2, #3 |
| 5 | MX cutover (Brad executes) | FUTURE | After #1-4 stable |
| 6 | Calendar export (Proton → .ics) | NOT STARTED | Need Proton access |
| 7 | Calendar structure in M365 (8 calendars) | NOT STARTED | Need M365 admin |
| 8 | Calendar import | NOT STARTED | Depends on #6, #7 |
| 9 | TickTick export → categorize → migrate | NOT STARTED | Need TickTick export |
| 10 | Contact consolidation (Proton, Android, Google, Contacts+, M365) | NOT STARTED | Need exports from David |
| 11 | OneDrive file organization | NOT STARTED | Need OneDrive access |
| 12 | Model routing: connect GPT-4o + Grok APIs | NOT STARTED | Need API keys from David |
| 13 | JR relaunch alignment (April 15) | IN PROGRESS | Active |
| 14 | Brad: WordPress email infra changes | NOT STARTED | Coordinate after #2-3 |
| 15 | Daily brief upgrade (calendar, tasks, cost) | READY | Implementing tomorrow |

---

## What I Can Do Now (No Blockers)

- Daily brief upgrade — add calendar conflicts, task priorities, cost tracking
- Model routing prep — architecture ready, need API keys
- TickTick categorization — once David exports
- Contact dedup logic — once David exports

## What I Need From David

1. **Proton admin access** (or forwarding configured by David) — for email forwarding + calendar export
2. **M365 admin access** — to create mailboxes, calendars, set Aaron as delegate
3. **TickTick export** — CSV file
4. **Contact exports** — from Proton, Android, Google, Contacts+
5. **GPT-4o API key** — for model routing
6. **Grok API key** — for model routing
7. **OneDrive access** — credentials or sharing

## What Brad Handles (After Email Infra Is Ready)

- SMTP cutover for JR + GJ WordPress sites
- Form submission validation (assessments, contacts)
- WooCommerce email flows (GJ orders, receipts)
- DNS/MX updates when approved
- Staging first, then production

## Sequencing

```
Phase 1a: Email (Proton → M365 forwarding, mailboxes, shared boxes)
Phase 1b: Calendar (export, build structure, import)
Phase 1c: Tasks (TickTick → ACTIVE_WORK.md + backlog)
Phase 1d: Contacts (consolidate, dedup, import to M365)
Phase 1e: Files (OneDrive organization)
Phase 1f: Model routing (GPT-4o + Grok connected)
Phase 2: Brad executes email infra changes (SMTP, DNS, MX)
Phase 3: Full cutover — Proton becomes archive only
```

---

## Rules

- No parallel systems
- No over-engineering
- No assumptions
- If it's not written, it doesn't exist
- Ask when missing information
