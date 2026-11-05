---
name: usage-skill-gap-check
description: >-
  Use when auditing repeated verbal instructions or long-chat re-teaching that
  should have been saved as a skill (or similar reusable recipe) to cut context
  reload.
---
# Usage skill-gap check

Audit **re-teaching instead of skills**. When the owner keeps restating how to do a task, or a long chat reloads the same procedure, the fix is usually a reusable skill (or equivalent recipe), not another long explanation. Skills keep behavior consistent across long conversations and cut context burn.

Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot (and chat/day when available).
2. Sample at most two high-share chats, with a small limit, looking for **repeated how-to** or **procedure reload**.
3. Note whether a matching skill already exists in the shared library; do not invent skill inventory beyond what you can see.

## Check A — same procedure taught again and again
**Tripwire (all hold):**
- The same multi-step procedure is explained or corrected ≥ 2 times in one period (or clearly restated across chats)
- No durable skill / recipe already captures that procedure (or the seat never loads it)
- The work is expected to recur

**Do not trip for:** one-off experiments; procedures that change every run; secrets that must not live in a skill.

**Actions (propose, wait for yes):**
- Ask the seat to write a short skill from the last good run (generic steps; personal ids stay in memory/routines)
- Next time, invoke the skill instead of re-pasting the sermon

**Tradeoff:** a few minutes to author; skill must stay generic enough to share.

## Check B — long chat keeps reloading procedure context
**Tripwire (any holds):**
- Mid-chat “remember how we do X” forces a full re-summary of a known procedure
- Or the same checklist is pasted into the thread ≥ 2 times

**Actions (propose, wait for yes):**
- Move the checklist into a skill; point at it
- Optionally keep a private skills repo / export if the owner wants skills preserved outside one product

**Tradeoff:** less ad-hoc tweaking inside one mega-thread.

## Check C — corrections never graduate
**Tripwire:** the owner keeps patching the same mistake in chat (“no, always do Y”) without updating a skill or standing instruction.

**Actions (propose, wait for yes):**
- Fold the correction into the skill or profile memory once, then stop re-litigating it

**Tradeoff:** a bad correction baked into a skill hurts until rewritten—so propose the text first.

## Report shape
Lead with PASS/FAIL per check that had enough evidence. At most one action per check. Say what they give up. Change nothing until the owner says yes.
