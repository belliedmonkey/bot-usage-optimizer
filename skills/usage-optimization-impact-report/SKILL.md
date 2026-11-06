---
name: usage-optimization-impact-report
description: >-
  Use when recording an owner-approved usage optimization or showing its
  effect over time; keep an intervention ledger and observed usage changes,
  and never invent token or cost savings.
---
# Optimization impact report

This is a presentation capability, not a usage waste tripwire. It complements usage visibility: visibility shows current consumption; this report records what changed after an owner-approved optimization and what usage movement was observed afterward. High usage alone does not prove waste, and a usage drop alone does not prove that a specific optimization caused it.

## Do not invent savings
- Never convert usage shares or quota percentages into tokens.
- Never report "saved N tokens" or a dollar saving you calculated yourself.
- Show money only when the platform usage report itself includes an amount, and then only as observed spend with that source's stated scope and period (for example a combined on-demand total). Label it observed spend, not savings.
- Never attribute all usage movement to one optimization. Other work in the same window can move totals and shares.
- Preserve missing values as unknown, never zero. If a comparison cannot be made, say why and keep the row unmeasured.
- Do not title a headline as savings. Prefer "observed change", "still observing", or "unmeasurable".

## Intervention ledger
When the owner accepts a concrete optimization, append one row immediately. Do not log a mere suggestion.

Each row includes:
- time in the owner's timezone, with that timezone labeled
- the check that found it (or "owner-requested" if they named the change)
- target: bot, routine, chat pattern, or other named object
- action taken
- expected mechanism, in plain words (fewer idle runs, shorter context, handoff to a cheaper executor)
- measurement status: `observing`, `compared`, or `unmeasurable`
- baseline snapshot: source, retrieval time, reporting period, source timezone, units and denominators

Reuse one durable ledger. Do not start a parallel log per chat.

## After each accepted optimization
1. Append the ledger row.
2. Take one usage snapshot through the platform's supported usage tools. On Grok Bot, load usage-review and read the platform usage report; record source, retrieval time, period, timezone, units and denominators. Convert displayed times to the owner's timezone and label it. On OpenBot, load `usage-adapter-openbot` and use its verified surface; keep the desktop page's local host analytics separate from organization API figures. Other platforms need their own supported adapter; do not claim one exists without testing it.
3. Create or update the existing impact report page on the host's supported page/report surface. On Grok Bot, load canvas and reuse the same page for later entries. If no real ledger row and no real snapshot exist yet, do not create an empty page.
4. Do not install polling, a watcher routine, or a new seat just to refresh the report.

## Comparison
- Compare only after a window that matches the baseline: same source, same metric, and the same window type.
- Report the observed change in the source's own units. Example: a named routine's share of all usage in the last 7 days moved from 18% to 3%.
- State that shares are relative to all usage in that window. A share can rise or fall because other work changed, not only because this optimization did.
- If an earlier period provides shares only, report shares. Do not call that a percent of that period's limit.
- Keep plan-wide quota usage distinct from one bot's or one routine's share. Never multiply percentages that have different denominators, and never mix incompatible windows.
- When comparison is impossible, leave status as `observing` or `unmeasurable` and explain the gap.

## Daily view
- Default: update the page when an optimization is recorded or the owner asks for a snapshot.
- Optional daily snapshot: at most once per day, and only after explicit owner opt-in. Tell them that each usage read itself consumes usage. Suggested starting point: evening in the owner's timezone, flexible. Confirm timezone when enabling.
- Do not enable this schedule merely by loading the skill.
- A daily snapshot, when enabled, adds that day's usage observation, new interventions from that day, rows still observing, and any newly comparable changes.
- If the scheduled run has no new intervention, no newly comparable window, and no owner-requested snapshot, do not perform an extra usage read just to say nothing changed.

## Delivery
- Label the page as a snapshot, not live. Show source, time, period and material limitations once.
- Keep observed usage separate from audit interpretation. Do not turn a drop into a savings claim.
- Controls on the page only filter or sort embedded data.
- Do not copy another product's UI or branding.
- Do not put personal bot names, usage snapshots, private links or credentials into public templates or repositories. Public packs ship this method and an empty schema only.

## Empty schema
Use these fields in public templates without sample personal values:

- `recordedAt`
- `timezone`
- `check`
- `target`
- `action`
- `expectedMechanism`
- `measurementStatus` (`observing` | `compared` | `unmeasurable`)
- `baseline` (`source`, `retrievedAt`, `period`, `sourceTimezone`, `units`, `denominators`)
- `comparison` (`source`, `retrievedAt`, `period`, `metric`, `before`, `after`, `notes`) or unknown
- `observedSpend` only when the source reported money, including its scope; otherwise omit

## Optional routine recipe (disabled by default)
Suggested schedule: once daily in the evening of the owner's confirmed timezone, flexible. Do not install this schedule merely by loading the skill.

Prompt intent:
If the owner enabled a daily optimization-impact snapshot, take at most one usage snapshot through supported tools and update the existing impact report page using usage-optimization-impact-report. Append no invented savings. Record only observed usage with source, period and denominators. Update rows whose comparable window is now available. If nothing new can be recorded and no snapshot was authorized for this run, end without an extra usage read.
Deliver a short owner notice only when a new intervention was recorded that day or a comparison became available; otherwise stay silent.
