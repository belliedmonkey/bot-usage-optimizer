---
name: usage-oversized-chat-check
description: >-
  Use when auditing chats that burn usage by packing whole pipelines into one
  ask, reloading the same context, scanning without a scope cap, or continuing
  work in a single chat that has grown long enough to reset.
---

# Usage oversized chat check

Audit chat habits that inflate a single conversation. Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot (and day if finding spikes). Prefer chat-level activity when the report includes it.
2. Inspect at most two high-share chats or transcripts, with a small limit, only when the bot name alone is not enough to judge value vs waste.
3. Judge from owner asks and bot behavior patterns — not from model names (the report does not split by model).
4. For Check D, note whether later work is still happening in one long-running thread rather than a fresh chat.

## Check A — one ask packs a whole pipeline
**Tripwire (any holds):**
- One request simultaneously demands research + multi-place edits + verification + an outbound send
- Or an explicit “do it all in one go” that spans 3+ independent goals

**Actions (propose, wait for yes):**
- Split into one deliverable step at a time
- Keep long work on the already-running line; avoid parallel restarts of the same job

**Tradeoff:** less mid-flight realtime feel.

## Check B — context reloaded again and again
**Tripwire (any holds):**
- Same material “read again / summarize again” ≥ 2 times in one session
- Or a short question pasted with a large block that could have been a pointer to an existing conclusion or file

**Actions (propose, wait for yes):**
- Point at the prior conclusion or file; ask only for the delta
- Default: do not reread the full source unless the owner names what to recheck

**Tradeoff:** occasional missed old detail; owner can point to reload once.

## Check C — exploration scope too wide
**Tripwire (any holds):**
- Unscoped “whole site / whole repo / everything recent” scans before success criteria exist
- Or one turn fans out multiple independent heavy investigations

**Actions (propose, wait for yes):**
- Set success criteria and hard caps first (pages, sources, time)
- Reuse the last report when it still answers; do not rerun by default

**Tradeoff:** narrower coverage; may need a second round.

## Check D — one chat that never resets
Later turns in a long conversation keep paying to reread earlier history. Some hosts can duplicate a seat or start a fresh chat that keeps the profile, skills, and routines and drops the history.

**Tripwire (all hold):**
- One conversation has kept growing across many turns or sessions, and later work still happens in that same thread
- That chat (or its bot) is a material share this period, or the owner is clearly continuing a long-running thread
- The host supports duplicating the seat or opening a fresh chat that keeps profile, skills, and routines and drops history

**Do not trip for:** a short or new chat; a thread the owner explicitly needs to keep intact for an investigation still in flight.

**Actions (propose, wait for yes):**
- First move durable decisions and state out of the chat (a short note or file the next chat can open)
- Then use the host's supported duplicate or fresh-chat action that keeps profile, skills, and routines and drops history. If the host has no such action, say so and stop; do not invent a button or menu path
- Continue the work in the fresh chat; leave the old thread unread unless the owner points at something in it

**Tradeoff:** earlier turns are no longer in context unless pointed at.

## How to report
- Use only names and figures from the usage report
- Offer at most three changes, largest waste first; say what changes, why, and what they give up
- Ask which to adopt; encode as owner preferences/memories only after an explicit yes
- Do not invent token counts or predicted savings
- Never suggest changing the host product’s built-in check-ins
