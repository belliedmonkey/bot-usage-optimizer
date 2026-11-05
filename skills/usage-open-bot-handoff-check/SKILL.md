---
name: usage-open-bot-handoff-check
description: >-
  Use when auditing whether a premium/cloud bot is doing whole tasks an
  open-source bot seat (e.g. OpenBot) could finish cheaper after receiving a
  clear issue/brief.
---
# Usage open-bot handoff check

Audit **handoff to cheaper open seats**. When an open-source bot product (for example OpenBot) can finish a job with a cheaper model, the premium/cloud bot should **write a clear issue or brief and hand it off**—not burn its own turns executing the whole task. Keep the premium seat for work that needs its connectors, signed-in consoles, or judgment the open seat cannot match.

Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot (and chat/day when available).
2. Note whether the owner already runs an open seat (OpenBot or similar) that can take issues.
3. Sample at most two high-share chats, with a small limit, only when needed to judge **fully executable open-seat work** vs **premium-only work**.

## Check A — premium seat executes what an open seat could own
**Tripwire (all hold):**
- A material share of recent premium/cloud-bot usage is long execution (research loops, drafting, coding support, repetitive ops) that does **not** require that seat’s exclusive consoles/connectors
- An open seat the owner already uses could run the same outcome with a cheaper model
- The premium seat did not stop at a short issue/brief + accept; it kept executing the full job

**Do not trip for:** high-ROI external console work that only the premium seat can drive; one-shot triage; accepting/rejecting open-seat output; jobs the open seat cannot reach (missing auth, missing tools).

**Actions (propose, wait for yes):**
- Premium seat writes a scoped **issue/brief** (goal, constraints, success checks, links) and hands it to the open seat
- Premium seat only re-enters to accept, remoke the issue, or handle blockers the open seat cannot

**Tradeoff:** one handoff step; open seat may need a sharper brief on the first remoke.

## Check B — handoff without a usable issue
**Tripwire (any holds):**
- Work was “handed off” as a vague ping or full transcript dump with no goal/success checks
- Or the open seat was woken only to re-read the same long context the premium seat already had

**Actions (propose, wait for yes):**
- Require a short issue shape: outcome, in/out of scope, success checks, pointers (not a full transcript)
- Forbid shuttling the same long chat back and forth “to sync”

**Tradeoff:** writing the issue takes a small premium-seat cost up front.

## Check C — open seat wrongly used for premium-only consoles
**Tripwire:** advice pushes **signed-in console / connector-only** jobs to an open seat that cannot finish them cheaper (or at all).

**Actions (propose, wait for yes):**
- Keep those jobs on the premium/cloud bot (see also [usage-bot-vs-harness-check](sand-workflow:usage-bot-vs-harness-check))
- Do not “save usage” by bouncing them into a dead end

**Tradeoff:** console work still spends premium usage—that is often correct.

## Report shape
Lead with PASS/FAIL per check that had enough evidence. At most one action per check. Say what they give up. Change nothing until the owner says yes.
