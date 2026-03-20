# External Research Protocol

**Status:** ACTIVE
**Date:** 2026-03-20

---

## Rules

1. **No independent research.** All external research starts with David.
2. **Precheck required.** When research is needed, STOP and prompt David with objective + specific queries.
3. **Use query library first** before crafting new queries.
4. **Transform, not repeat.** Compress → Evaluate → Adapt → Improve → Output → Store.
5. **Perplexity = raw input. Aaron = refinement + execution.**
6. **Never treat Perplexity as truth.** Never copy wording. Never skip adaptation.
7. **Future Aaron-Research agent follows this same protocol.**

---

## Precheck Prompt Format

```
David — external research needed.

Objective:
[clear objective]

Go to Perplexity and run this:

[query or queries]

Return results and I will process them.
```

---

## Query Library

### Joy Restart (Primary)
1. "best funnels for Christian assessments that convert to coaching or community with email follow-up sequences"
2. "examples of re-engagement email sequences for inactive email lists in coaching or ministry platforms"
3. "how personality or spiritual assessments convert users into paid coaching or community membership"
4. "best practices for assessment result reports that increase user action and next step conversion"
5. "how to structure webinars that convert attendees into coaching or online community memberships"

### Generous Java
6. "how churches use coffee or products for fundraising and recurring revenue models"
7. "best subscription coffee business models and customer retention strategies"
8. "how small coffee brands scale through wholesale and church partnerships"

### BAG (Consulting)
9. "how AI consulting firms package services for small to mid-sized businesses"
10. "best lead generation strategies for boutique consulting firms with multiple verticals"

### General Strategy
11. "how to structure a clear offer ladder from free to paid services in coaching or ministry businesses"
12. "how online communities grow and retain engagement in coaching or faith-based platforms"

---

## Ingestion Process

When David sends research results:

1. **COMPRESS** — summarize key insights, remove redundancy
2. **EVALUATE** — useful vs generic, missing, wrong
3. **ADAPT** — map to JR / GJ / BAG / etc.
4. **IMPROVE** — make it better, align with David's voice
5. **OUTPUT** — key insights (short), what matters (prioritized), specific actions, next steps
6. **STORE** — write to `notes/research/perplexity_insights_YYYY-MM-DD.md`

---

## Restrictions

- Do NOT treat Perplexity as truth
- Do NOT copy wording
- Do NOT over-research
- Do NOT skip adaptation
- Do NOT access restore archive without explicit approval
