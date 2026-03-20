# WORKFLOWS.md — Controlled Workflow Execution

## Rules
- No autonomous workflows — only execute defined and David-approved workflows
- Workflows are explicit, not dynamic — every step is written before execution
- Results must be written to disk
- New workflows require David's approval before first execution

---

## WF-001: JR Assessment Audit

**Objective:** Audit Joy Restart assessment experience end-to-end as a user — document UX, report quality, conversion points, and gaps.

**Tools required:** Browser (Chromium headless), web_fetch, file write

**Steps:**
1. Navigate to joyrestart.com/assessments/
2. Click into Joy Assessment
3. Document: registration flow, question format, friction points, clarity
4. Complete the assessment
5. Document: report delivery method, report content, quality, tone
6. Evaluate: what next-step CTAs appear after the report
7. Rate: is the path to community/coaching/resources obvious and compelling?
8. Repeat steps 2-7 for Fear Assessment
9. Compare: consistency between Joy and Fear experiences
10. Write findings to notes/jr_assessment_experience_2026-03-20.md
11. Identify: top 3 high-impact improvements
12. Commit

**Output:** notes/jr_assessment_experience_2026-03-20.md

**Status:** READY — blocked on David providing assessment access credentials or confirming Aaron can register as a test user

---
