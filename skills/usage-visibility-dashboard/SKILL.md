---
name: usage-visibility-dashboard
description: >-
  Use when the owner wants to see where bot usage goes: an on-demand dashboard
  by bot and activity, with explicit periods, denominators and evidence gaps.
---
# Usage visibility dashboard

Make usage understandable before suggesting cuts. This is a presentation capability, not a waste tripwire. High usage alone does not prove waste.

## Evidence
- Obtain one current usage report through the platform's supported tools or an owner-supplied export. On Grok Bot, load usage-review and use CheckSubscriptionUsage. Other platforms need their own supported adapter; do not claim one exists without testing it.
- Record source, retrieval time, reporting period, source timezone, reset time if provided, units and denominators. Convert displayed times to the owner's timezone and label it.
- Keep plan-wide limit usage distinct from this product's usage and each bot's share. Never multiply percentages with different denominators or combine current-week totals with last-seven-days activity.
- Preserve null/missing values as unknown, never zero. If no usable data exists, explain what is missing; do not draw a fabricated dashboard.

## Views
1. Show quota used and reset only if present, with their scope explicit.
2. Rank bots by usage using the report's actual metric and period. Use horizontal bars and a compact table; long tails may be grouped as Other with the rule stated.
3. Show chats, routines and bot-to-bot activity when the source supplies those categories. Keep any unknown/unclassified remainder explicit.
4. Use stacked bars per bot only when bot-by-activity joint values are actually provided. Never infer a joint distribution from two separate marginal totals.
5. A bot-to-activity flow diagram is optional, only when real joint values exist and it adds clarity over stacked bars. Reconcile totals within stated source rounding; omit the flow otherwise.
6. Show day trends or period comparisons only for compatible measurements and matching windows. Do not predict exhaustion or savings from percentage shares alone.

## Delivery
- Produce a dashboard in the host's supported page/report surface. On Grok Bot, load canvas and follow its rules; reuse the existing usage page for later snapshots. Else use an available dashboard surface or a portable report, explaining substitutions.
- Label it as a snapshot, not auto-live. Show source/time/period and material limitations once, with no decorative empty panels.
- Controls only filter/sort embedded data. Refresh requires a new source read requested by the owner; do not install polling, routines or a new seat just to refresh the dashboard.
- Keep observed usage separate from audit interpretation. Offer at most three evidence-backed follow-up checks; sampled evidence is needed to call something waste. Make no configuration changes without approval.
- Do not copy another product's UI or branding. Do not put personal bot names, usage snapshots, private links or credentials into public templates or repositories.
