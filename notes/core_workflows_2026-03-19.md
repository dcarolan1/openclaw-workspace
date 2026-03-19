# Core Operational Workflows — 2026-03-19

## Overview

Seven workflows that cover David's recurring operational needs across BAG, E456 (church — parent of Joy Restart and Generous Java), Sunny Antiques, KNGD VNTRS, Rhythm.Coffee, Ekklesia of Texas, and shared functions. Each workflow defines what Aaron does, what David does, and which model handles each step.

---

## 1. Partner & Client Outreach

**Businesses:** BAG, Generous Java, Joy Restart
**Trigger:** David says "reach out to [person/org] about [topic]" or Aaron identifies an opportunity during research/monitoring.

**Inputs required:**
- Target name/org
- Purpose (partnership, client, vendor, sponsor)
- Context (how David knows them, what the angle is)
- Urgency (now vs. next batch)

**Execution:**

| Step | What Aaron does | Model | Autonomy |
|------|----------------|-------|----------|
| 1. Research target | Look up org, person, recent news, social presence | qwen3:8b (quick lookups) + web search | Autonomous |
| 2. Draft outreach brief | One paragraph: who they are, why they matter, suggested angle | qwen3:32b | Autonomous |
| 3. Present to David | Send brief via Telegram with recommendation | — | David approves/adjusts |
| 4. Draft message | Write email or WhatsApp message in David's voice | Claude (high-stakes writing) | David approves before send |
| 5. Send | Deliver via email or WhatsApp | — | Autonomous after approval |
| 6. Log | Record outreach in daily log + contact tracker | qwen3:8b | Autonomous |

**Output:** Sent message + logged record
**Storage:** `memory/YYYY-MM-DD.md` + `notes/outreach/[org-name].md` (if ongoing relationship)

---

## 2. Content Creation

**Businesses:** BAG (blog, thought leadership), Joy Restart (stories, updates), Generous Java (product, brand), E456 (devotionals, ministry)
**Trigger:** David requests content, calendar says content is due, or Aaron identifies a content opportunity.

**Inputs required:**
- Topic or theme
- Audience (clients, donors, customers, congregation)
- Format (blog post, social post, newsletter section, devotional)
- Tone guidance (if different from default)

**Execution:**

| Step | What Aaron does | Model | Autonomy |
|------|----------------|-------|----------|
| 1. Research/gather | Pull relevant context, prior content, audience info | qwen3:8b + web search | Autonomous |
| 2. Outline | Structured outline with key points, 3-5 bullets | qwen3:32b | Autonomous |
| 3. Draft | Full draft in appropriate voice and format | Claude (final-quality writing) | Autonomous |
| 4. Present to David | Send draft via Telegram | — | David approves/edits |
| 5. Finalize | Incorporate David's feedback, produce final version | Claude | Autonomous |
| 6. Store | Save final to workspace, log in daily notes | — | Autonomous |

**Output:** Final content piece, ready to publish
**Storage:** `content/[business]/[YYYY-MM-DD]-[topic-slug].md`

**Note:** For E456/ministry content, David may want more direct involvement in drafting. Respect that — present outline, get direction, then draft.

---

## 3. Research & Synthesis

**Businesses:** BAG (client research, market analysis), all (competitive intel, opportunity identification)
**Trigger:** David asks a question, needs background for a meeting, or Aaron identifies a knowledge gap during other work.

**Inputs required:**
- Question or topic
- Depth (quick answer vs. full brief)
- Context (why David needs this, what decision it informs)

**Execution:**

| Step | What Aaron does | Model | Autonomy |
|------|----------------|-------|----------|
| 1. Scope | Clarify what's needed if ambiguous | — | Back-and-forth (only if unclear) |
| 2. Search & gather | Web search, fetch relevant sources, extract key info | qwen3:8b (fast extraction) + web tools | Autonomous |
| 3. Analyze | Synthesize findings, identify patterns, form conclusions | Claude (reasoning quality matters) | Autonomous |
| 4. Write brief | Structured brief: summary → key findings → recommendation → sources | qwen3:32b (structured writing) | Autonomous |
| 5. Deliver | Send via Telegram. Short answer first, full brief attached as file if long. | — | Autonomous |
| 6. Store | Save brief to workspace | — | Autonomous |

**Output:** Research brief (short Telegram summary + full document if needed)
**Storage:** `notes/research/[YYYY-MM-DD]-[topic-slug].md`

**Quick vs. deep:**
- Quick (< 5 min): Answer directly in Telegram, log in daily notes
- Deep (investigation): Full brief, stored as standalone document

---

## 4. Assessment & Report Generation

**Businesses:** BAG (client deliverables), Joy Restart (impact reports, grant applications)
**Trigger:** David says "prepare a report on [topic]" or a client deliverable is due.

**Inputs required:**
- Subject/scope
- Audience (client, board, funder, internal)
- Data sources (what to pull from)
- Format requirements (if any)

**Execution:**

| Step | What Aaron does | Model | Autonomy |
|------|----------------|-------|----------|
| 1. Gather data | Collect inputs from workspace, web, or provided sources | qwen3:8b | Autonomous |
| 2. Process/analyze | Structure data, identify trends, calculate metrics if needed | qwen3:32b (local, private data) | Autonomous |
| 3. Draft report | Full report with exec summary, findings, recommendations | Claude (quality + reasoning) | Autonomous |
| 4. Format | Clean markdown or requested format | qwen3:8b | Autonomous |
| 5. Present to David | Send via Telegram with summary of key findings | — | David reviews, approves |
| 6. Revise | Incorporate feedback | Claude | Autonomous after direction |
| 7. Finalize & store | Final version to workspace, ready for delivery | — | Autonomous |

**Output:** Complete report document
**Storage:** `deliverables/[business]/[YYYY-MM-DD]-[report-name].md`

**Private data rule:** Any report involving sensitive client or financial data uses qwen3:32b for processing steps. Data never leaves the box unless David explicitly approves.

---

## 5. Product & Offer Development

**Businesses:** BAG (service packages, consulting offers), Generous Java (products, bundles), Joy Restart (programs)
**Trigger:** David says "I want to build [offer/product]" or Aaron identifies a market opportunity.

**Inputs required:**
- Concept or idea
- Target audience
- Constraints (budget, timeline, resources)
- Competitive context (optional, Aaron can research)

**Execution:**

| Step | What Aaron does | Model | Autonomy |
|------|----------------|-------|----------|
| 1. Research market | Competitive landscape, pricing, audience needs | qwen3:8b + web search | Autonomous |
| 2. Draft concept brief | One-page: what it is, who it's for, why now, pricing model, differentiation | Claude (strategic thinking) | Autonomous |
| 3. Present to David | Send brief via Telegram | — | Back-and-forth (this is collaborative) |
| 4. Iterate | Refine based on David's direction | Claude | Back-and-forth |
| 5. Build collateral | Landing page copy, pitch deck outline, email sequence | Claude (writing) + qwen3:32b (structured work) | David approves final |
| 6. Store | Save all artifacts to workspace | — | Autonomous |

**Output:** Concept brief + supporting collateral
**Storage:** `projects/[business]/[offer-name]/`

**Note:** This is the most collaborative workflow. David has strong opinions on products and offers. Present options with a recommendation, but expect iteration.

---

## 6. Email & Newsletter Communication

**Businesses:** BAG (client updates, thought leadership), Joy Restart (donor updates), Generous Java (customer newsletters)
**Trigger:** Scheduled cadence, David requests a send, or a notable event worth communicating.

**Inputs required:**
- Audience segment
- Topic or theme
- Key message / CTA
- Any links or resources to include

**Execution:**

| Step | What Aaron does | Model | Autonomy |
|------|----------------|-------|----------|
| 1. Gather content | Pull from recent work, content library, news | qwen3:8b | Autonomous |
| 2. Draft newsletter | Full draft with subject line, body, CTA | Claude (quality writing for external audience) | Autonomous |
| 3. Present to David | Send draft via Telegram | — | David approves before send |
| 4. Finalize | Incorporate any edits | qwen3:8b (quick edits) | Autonomous |
| 5. Prepare for send | Format for email platform, stage for delivery | — | Autonomous |
| 6. Log | Record what was sent, to whom, when | — | Autonomous |

**Output:** Ready-to-send newsletter/email
**Storage:** `content/[business]/newsletters/[YYYY-MM-DD]-[subject].md`

**Rule:** Nothing goes to an external audience without David's approval. No exceptions.

---

## 7. System & Build Tasks

**Businesses:** Cross-cutting (infrastructure, automation, tooling)
**Trigger:** David requests a build, Aaron identifies a system improvement, or a workflow needs automation.

**Inputs required:**
- What needs to be built or fixed
- Priority (now vs. backlog)
- Constraints (tools available, permissions needed)

**Execution:**

| Step | What Aaron does | Model | Autonomy |
|------|----------------|-------|----------|
| 1. Scope | Define what needs to happen, identify blockers | Claude (reasoning) | Autonomous |
| 2. Plan | Write implementation plan with steps | qwen3:32b | Autonomous |
| 3. Build | Write code, config, scripts | Claude (complex) or qwen3:8b (simple) | Autonomous |
| 4. Test | Verify it works | — (direct execution) | Autonomous |
| 5. Report | Tell David what was done, what changed | — | Autonomous |
| 6. Document | Update TOOLS.md, workspace docs as needed | qwen3:8b | Autonomous |
| 7. Commit | Git commit with clear message | — | Autonomous |

**Output:** Working system/automation + documentation
**Storage:** Workspace files + `notes/ACTIVE_WORK.md` update

**Autonomy note:** Routine system tasks (git commits, file organization, config tweaks) are fully autonomous. Anything that changes external-facing behavior or requires sudo gets David's approval first.

---

## Autonomy Summary

| Level | What qualifies | Examples |
|-------|---------------|----------|
| **Fully autonomous** | Internal work, research, drafting, filing, system maintenance | Research briefs, first drafts, git commits, file organization, daily logs |
| **David approves** | Anything external-facing or high-stakes | Outreach messages, newsletters, reports to clients, system changes with external impact |
| **Back-and-forth** | Strategic/creative decisions where David's judgment is essential | Product concepts, offer development, major content direction |

---

## Model Routing Summary

| Model | When to use |
|-------|-------------|
| **qwen3:8b** | Quick lookups, data extraction, formatting, simple edits, fast first passes |
| **qwen3:32b** | Private data processing, structured writing, analysis where data stays local |
| **Claude Opus** | Final-quality writing, complex reasoning, strategic thinking, anything David or clients will read |

**Rule of thumb:** Start fast (8b), upgrade to quality (32b) for structured work, go to Claude for anything that needs to be sharp. Never send qwen output directly to an external audience.

---

## Storage Convention

```
workspace/
├── content/[business]/           — published content
├── deliverables/[business]/      — client/external deliverables
├── projects/[business]/[name]/   — active project artifacts
├── notes/research/               — research briefs
├── notes/outreach/               — relationship tracking
├── memory/YYYY-MM-DD.md          — daily execution log
└── notes/ACTIVE_WORK.md          — priorities and task tracking
```

Create directories as needed. Don't pre-create empty structure.
