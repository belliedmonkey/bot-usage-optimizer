---
name: usage-routine-idle-check
description: >-
  Use when auditing scheduled or event routines for over-frequency, idle
  polling, unfiltered subscriptions, or cron used where an event trigger fits.
---
# Usage routine idle check

Audit scheduled and subscription routines for waste. Prefer proactive routines, but **frequency and filters** matter: scheduled ones should rarely fire more often than hourly; subscription/event ones should filter first. Numbers come only from a platform usage report supplied by an adapter. This checklist does not include an adapter. If no report is in hand, say so and stop. Never invent usage numbers; never add a routine whose only job is watching usage.

## Data to pull
1. From the platform usage report, read usage grouped by bot and routine (current week). If shares look empty right after reset, use the last 7 days window the same way.
2. For each candidate routine, read its saved prompt and schedule/trigger (get before edit).
3. Sample recent outputs only when needed to judge sameness — keep reads small.

## Check A — almost unchanged, still polled daily
**Tripwire (all must hold):**
- Frequency ≥ once per day, or the usage report’s about-weekly run count ≥ 5
- Last 3 outputs have the same material conclusion, or ≥ 2 of them are clearly “no change / nothing to report”
- Not a real-time / on-call disposition job (nobody acts right when it finishes)

**Do not trip for:** compliance or safety deadline reminders; KPIs the owner explicitly requires daily.

**Action ladder (propose, wait for yes):**
1. Keep only weekday daytime runs; otherwise move to 2–3 times per week
2. If still almost unchanged for two weeks → once per week or pause (prefer pause over delete)

**Tradeoff:** fresher results.

## Check B — event-shaped work on a cron idle loop
**Tripwire (all must hold):**
- The job’s meaning is “only when something new happens” (message, PR/push, comment, email, status change, and similar)
- It runs on a schedule/cron today, and in about the last week idle runs (nothing new to report) are ≥ 50%, **or** about-weekly runs ≥ 7 with mostly empty reports
- A matching event trigger exists for that job (Slack, GitHub, email, and similar, per that platform’s trigger list)

**Do not trip for:** intentional rollup digests; multi-source jobs with no single event source; triggers the platform cannot express.

**Actions (propose, wait for yes):**
- Trigger source connected → switch to event trigger; stop the equivalent cron
- Not connected yet → cut to ≤ 2–3 runs per week and name the connector gap; do not pretend the trigger is done

**Tradeoff:** short setup; the app must be connected for a full switch.

## Check C — scheduled cadence hotter than needed
**Tripwire (any holds):**
- A scheduled/cron routine fires more often than **hourly** (e.g. every 5–30 minutes) without an on-call disposition need
- Or about-weekly run count is extreme for a digests/watch job that could be hourly or less

**Do not trip for:** true on-call / live-meeting jobs the owner named as time-critical.

**Actions (propose, wait for yes):**
- Cap scheduled routines at ≤ hourly unless the owner explicitly needs hotter
- Prefer event/subscription triggers over hot cron when the platform allows

**Tradeoff:** slightly slower awareness between events.

## Check D — subscription / event routine without a filter
**Tripwire (all hold):**
- The routine is event- or subscription-driven (email, Slack, GitHub, webhook, and similar)
- It fires on a broad stream (all mail, all channel messages, all repo events) with little or no filter in the trigger or prompt
- Recent runs show high idle or low-value volume relative to useful actions

**Actions (propose, wait for yes):**
- Narrow the trigger (sender, label, repo, event type, channel) before keeping the subscription
- Keep “summarize and file” jobs only on the filtered subset

**Tradeoff:** might miss edge events outside the filter—widen only with evidence.

## How to report
- Use only names and figures from the usage report
- Offer at most three changes, largest waste first; for each say what changes, why, and what they give up
- Ask which to apply; change only after an explicit yes
- Prefer pause over delete; get a routine before editing its prompt or schedule
- You can change only this auditor’s own routines; for another bot’s, tell the owner where, or ask that bot if they want
- Never suggest changing the host product’s built-in check-ins
