---
name: review-checklist
description: Reviews a product brief against the PM's six-point checklist before it goes any further. Use when the user says "review this brief", "run the review checklist", "check this brief", or points at a brief (file, wiki page or pasted text) and wants it checked.
---

# Review checklist

Check one brief against the six points below, the same way every time. Review only; do not rewrite the brief unless asked.

## Input

The brief is whatever the user points at: a file path, a wiki page, or pasted text. If it is not clear which brief, ask. Read the whole brief before judging any point.

## The six checks

1. **Current customer experience is explained.** The brief describes what the customer does and sees today, in concrete terms, not just what they will get.
2. **The problem is identified and explained.** The brief names the problem and says why it matters and who has it. Evidence counts (data, tickets, interviews); assertion alone is weaker.
3. **It names who owns it.** One named person or role is accountable for the work. A team name or "TBD" does not count.
4. **It says how we'll know it worked.** There is a measurable success signal (metric, target or observable outcome), not just "improve X".
5. **Scope at the end matches scope at the start.** Compare what the opening says the brief covers with what the closing sections, requirements or asks actually deliver. Flag anything added, dropped or quietly widened between the two.
6. **The problem comes before the fix.** The problem is explained before any solution is proposed. Flag solutions that appear earlier than the problem or that stand in for it.

## How to judge

Give each check one of:
- **Pass**: clearly met.
- **Partly**: present but thin, vague or out of place.
- **Missing**: not there.

Back every rating with a short pointer to where in the brief you found it (section name or a few words quoted), or say it is absent. Do not give credit for things the brief implies but never says. Do not invent facts to fill gaps.

## Output

Use this format:

**Brief:** <title or path>

| # | Check | Rating | Evidence |
| --- | --- | --- | --- |
| 1 | Current customer experience | Pass / Partly / Missing | ... |
| 2 | Problem identified and explained | ... | ... |
| 3 | Owner named | ... | ... |
| 4 | Success measure | ... | ... |
| 5 | Scope start matches end | ... | ... |
| 6 | Problem before fix | ... | ... |

**Verdict:** one sentence: ready to move on, or not yet, and why.

**To fix before it goes further:** a short list, one line per Partly or Missing item, saying what to add or change. Omit if everything passes.
