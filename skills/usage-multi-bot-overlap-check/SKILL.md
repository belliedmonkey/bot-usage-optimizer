---
name: usage-multi-bot-overlap-check
description: >-
  Use when auditing waste from several bots or agents working the same job at
  once, bot-to-bot re-forwarding, broadcast @-mentions, or a large thin team
  instead of a few good seats.
---
# Usage multi-bot overlap check

Audit parallel-bot waste. A **few good seats** are usually easier to manage and cheaper than a large thin team. Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot (and by activity when available, especially bot-to-bot and group chats).
2. Name the two or three bots with the largest shares. Only open at most two transcripts when a name is not enough to judge overlap.
3. Count how many seats show material usage this period (not zero / noise-only).
4. Do not blame models; the report does not split by model.

## Check A — same job started on multiple seats
**Tripwire (all hold):**
- The same workstream is handed to ≥ 2 bots in a short window
- Their goals overlap (all researching, changing, or watching the same outcome)

**Actions (propose, wait for yes):**
- Keep one owner seat that closes the loop; other seats join only when named
- Bystander seats must not rerun the same investigation on their own

**Tradeoff:** less realtime side observation.

## Check B — bot-to-bot reforward / reread
**Tripwire (any holds):**
- Bot-to-bot share looks high among usage for the period
- Or the same conclusion is pasted/woken across seats ≥ 2 times only to “sync”

**Actions (propose, wait for yes):**
- Owner seat delivers once; cross-seat handoff is one clear brief, not a full context dump
- Forbid shuttling the same long transcript back and forth

**Tradeoff:** other seats have thinner context unless the owner points them at what to load.

## Check C — broadcast @-mentions fan out duplicates
**Tripwire (any holds):**
- One instruction @-mentions multiple seats with overlapping roles
- Or a group thread’s follow-ups cause several seats to re-investigate the same question

**Actions (propose, wait for yes):**
- Group chat sets direction only; execution moves to a single seat’s private chat

**Tradeoff:** less shared visibility while work runs.

## Check D — large thin team instead of a few good seats
**Tripwire (all hold):**
- Many seats show material usage this period (rule of thumb: ≥ 6), **or** several seats each hold a thin slice of the same domain
- Two or more of those seats have overlapping goals / descriptions / top chats
- No clear “one owner per workstream” map the owner already enforced

**Do not trip for:** deliberately separated domains (e.g. App vs site vs machine-ops) with low overlap; a designer/onboarding helper that rarely executes the same jobs.

**Actions (propose, wait for yes):**
- Merge or pause thin overlapping seats; keep a small set of strong owners
- Route new work to an existing owner before creating another seat

**Tradeoff:** less specialty branding per seat; one owner carries more of that domain.

## How to report
- Use only names and figures from the usage report
- Offer at most three changes, largest waste first; say what changes, why, and what they give up
- Ask which to adopt; write shared/owner preferences only after an explicit yes
- Messaging another bot to change its routines also uses usage — say so before offering
- Never suggest changing the host product’s built-in check-ins
