---
name: usage-script-vs-chat-check
description: >-
  Use when auditing chat/cloud-bot turns spent repeatedly doing a workflow that
  a small script (plus a thin skill) would finish with far fewer tokens.
---
# Usage script vs chat check

Audit **chat doing what a script should**. For repeatable workflows, a small script (stored in a private repo when useful) plus a thin skill is usually much cheaper than the bot re-walking the same steps in chat every time. The bot still plans, generates, and accepts the script—it should not keep being the runtime for the whole loop.

Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot (and chat/day when available).
2. Sample at most two high-share chats for **the same mechanical workflow** re-run in chat (export→transform→upload, poll→format→post, batch renames, and similar).
3. Note whether a local harness / open seat already exists to host scripts (see also [usage-bot-vs-harness-check](sand-workflow:usage-bot-vs-harness-check) and [usage-open-bot-handoff-check](sand-workflow:usage-open-bot-handoff-check)).

## Check A — repeatable workflow still runs as chat turns
**Tripwire (all hold):**
- The same mechanical multi-step workflow ran in chat ≥ 2 times with little judgment variance
- Steps are mostly deterministic (API/CLI/file transforms) rather than open-ended research
- No script/skill pair already owns that workflow

**Do not trip for:** first-time exploration; workflows that change shape every run; console jobs that need interactive signed-in sessions the script cannot hold.

**Actions (propose, wait for yes):**
- Ask which parts should become a script; bot writes the script + a short skill that invokes it
- Store scripts in a private repo if the owner wants them preserved outside one product
- Later runs: skill → script (or harness/open seat runs the script); bot only accepts exceptions

**Tradeoff:** upfront authoring; scripts need light maintenance when APIs change.

## Check B — bot re-implements the script in prose every time
**Tripwire:** each run re-derives the same commands/checklist in chat instead of calling a saved script/skill.

**Actions (propose, wait for yes):**
- Freeze the last good command path into a script; point the skill at it
- Forbid “just do it in chat once more” when the script already exists unless the owner is debugging the script

**Tradeoff:** less mid-flight improvisation inside the happy path.

## Check C — script work stuck on the expensive seat
**Tripwire:** script authoring or repeated script runs burn the premium/cloud seat when a local harness or cheaper open seat could run them after a brief.

**Actions (propose, wait for yes):**
- Premium seat writes the issue/brief + success checks; harness/open seat runs the script work; premium seat accepts

**Tradeoff:** one handoff; keep console-only pieces on the premium seat.

## Report shape
Lead with PASS/FAIL per check that had enough evidence. At most one action per check. Say what they give up. Change nothing until the owner says yes.
