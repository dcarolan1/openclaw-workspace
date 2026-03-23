# Model Routing Protocol v1 + Task Tagging System

**Status:** ACTIVE
**Date:** 2026-03-23
**Goal:** Reduce cost ~50%, maintain/improve quality, zero decision friction

---

## Tags

| Tag | Meaning | Model | Example |
|-----|---------|-------|---------|
| [Q] | Quick — low stakes, fast | qwen3:8b only | Rewrites, formatting, short summaries |
| [W] | Work — moderate depth, internal | qwen3:32b (Claude optional) | Analysis, structured writing, reports |
| [F] | Final — David/public-facing | 8b/32b draft → Claude finish | Emails, partner outreach, published content |
| [T] | Thinking — high judgment | Claude first (32b optional after) | Strategy, theology, system design, decisions |

## Flow

Draft (8b) → Build (32b) → Finalize (Claude)

## Hard Rules

1. No Claude for first drafts
2. No skipping layers (idea → Claude is prohibited)
3. Stop early if 8b output is sufficient
4. Claude once per final pass — no loops unless justified
5. Compress context before Claude — minimal input, maximum clarity

## Daily Brief Addition

- Tasks by tag (Q/W/F/T)
- Where Claude was used
- Where Claude was avoided
- Routing improvement notes

## Override

If quality is at risk → escalate to Claude → note why
