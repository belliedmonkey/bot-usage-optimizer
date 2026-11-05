---
name: usage-bot-vs-harness-check
description: >-
  Use when auditing whether cloud/chat bots are burned on local heavy work
  (coding, builds, smoke) that a local harness should run, while keeping
  high-ROI external console tasks on the bot.
---
# Usage bot vs harness check

Audit **where work runs**. Cloud/chat bots are usually strongest at **external control-plane / console tasks** (Search Console, Trends, cloud consoles, Amazon seller/ops, ads, ASC, and similar signed-in web work). That work often has high value per turn. **Local heavy work**—editing code, installs, long builds, smoke, real-device screenshots—usually has better cost/performance on a **local harness** (for example `dsh`, OpenCode, or another on-machine coding agent).

Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot (and by chat/day when available).
2. Sample at most two high-share chats or transcripts, with a small limit, only when the bot name alone is not enough to judge **console work** vs **local heavy loops**.
3. Note any standing rule that already says “bot plans / harness executes.” Do not invent one.

## Check A — local heavy work stuck on the cloud bot
**Tripwire (all hold):**
- A material share of recent chat usage is long edit/build/test/smoke/screenshot loops on the user’s machine or repo
- The same outcome could be briefed to a local harness the owner already uses
- The bot is not only planning/accepting—it is repeatedly doing the concrete local steps itself

**Do not trip for:** short planning briefs; one-shot accept/reject of harness output; tiny reversible text tweaks the owner explicitly wants in-chat.

**Actions (propose, wait for yes):**
- Keep the bot on outcome + brief + accept; hand concrete local steps to the harness
- Cap cloud-bot retries of the same local failure; remoke the harness brief instead of re-burning the chat seat

**Tradeoff:** less “watch every keystroke in chat”; harness output must still be verified.

## Check B — high-ROI console work wrongly pushed off the bot
**Tripwire (any holds):**
- Owner (or another seat) is moving **external console / SaaS control-plane** jobs to a local harness that has no durable signed-in session or connector for that console
- Or advice treats those console jobs as “waste” only because they use chat turns

**Do not trip for:** console jobs that are pure API/CLI with a working local credential path the owner prefers.

**Actions (propose, wait for yes):**
- Keep those console tasks on the chat/cloud bot (or its connectors/browser)
- Do not “save usage” by bouncing them to a harness that cannot finish them cheaper

**Tradeoff:** console work still spends chat/cloud usage—that is often the intended spend.

## Check C — mixed asks in one seat
**Tripwire:** one request mixes **console ops** and **local heavy coding** with no split.

**Actions (propose, wait for yes):**
- Split: bot (or owning seat) runs the console part; harness runs the local heavy part; bot accepts both against success checks

**Tradeoff:** one extra handoff line between seats/tools.

## Report shape
Lead with PASS/FAIL per check that had enough evidence. At most one action per check. Say what they give up. Change nothing until the owner says yes.
