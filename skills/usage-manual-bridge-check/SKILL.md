---
name: usage-manual-bridge-check
description: >-
  Use when auditing copy-paste or hand bridges between apps and the bot that a
  connector, vault, or bot-owned account should close.
---
# Usage manual-bridge check

Audit **hand bridges**. If the owner still copies and pastes between tools and the bot—or re-types what another app already knows—that burns turns and context. Prefer connectors, vault/credentials, and (when useful) a bot-owned email/account so the bot can finish the loop itself.

Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot (and chat/day when available).
2. Sample at most two high-share chats for **paste dumps**, **“here is what I copied from …”**, or repeated export→paste→ask cycles.
3. Note which connectors/vault entries already exist; do not invent access.

## Check A — copy-paste is the integration
**Tripwire (all hold):**
- The same path shows paste of app output into chat ≥ 2 times (or a large paste that could have been a connector/API read)
- A connector, export path, or vault login for that app is available or installable
- The job is recurring, not a one-off screenshot of something broken

**Do not trip for:** one-time pastes to debug; content the bot must not store; apps with no safe connector the owner refuses.

**Actions (propose, wait for yes):**
- Connect the app (or vault login) and let the bot read/write through tools
- Replace “paste me the page” with a named tool call in the skill

**Tradeoff:** setup time; connector scope must match what the owner allows.

## Check B — credentials typed or pasted each time
**Tripwire (any holds):**
- Logins, codes, or addresses are re-pasted into chat instead of vault / fill-credential flows
- Or the bot asks for the same contact/card details every run

**Actions (propose, wait for yes):**
- Save once in vault; use vault/fill paths thereafter
- Never keep secrets in skills or memory prose

**Tradeoff:** vault approval clicks on first use.

## Check C — bot could own the loop but stays a paste sink
**Tripwire:** the workflow needs a dedicated inbox or account for sign-ups/notifications, and the owner is still forwarding those by hand into chat.

**Actions (propose, wait for yes):**
- Give the bot its own email/address where the product supports it, and wire that inbox
- Keep human approval on sends and purchases

**Tradeoff:** another inbox to watch; separation is the point.

## Report shape
Lead with PASS/FAIL per check that had enough evidence. At most one action per check. Say what they give up. Change nothing until the owner says yes.

Related: [usage-oversized-chat-check](sand-workflow:usage-oversized-chat-check) for reload patterns; [usage-skill-gap-check](sand-workflow:usage-skill-gap-check) when the missing piece is a recipe, not a connector.
