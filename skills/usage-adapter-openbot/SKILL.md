---
name: usage-adapter-openbot
description: >-
  Read one current OpenBot usage report through a verified surface, record source,
  period, timezone and units, and hand it to the visibility dashboard or impact report.
---
# OpenBot usage adapter

Thin read skill. This is not a waste tripwire and it does not schedule or poll anything.

## When to use

Use when the owner asks to see OpenBot usage, rank OpenBot bots or agents, check OpenBot
credits or budgets, or measure an OpenBot optimization. Load `usage-visibility-dashboard` for
the picture and `usage-optimization-impact-report` only when a comparable baseline exists.

## 1. Pick a supported surface

Prefer, in order:

1. **Organization API** — `GET /v1/organization/usage` (summary), `/usage/events` (per-call
   detail), `/credits` (organization balance), and `/budgets` (limits and spend). Use the
   origin of the OpenBot server being audited. Do not use the docs' `api.example.com`
   placeholder. The hosted 0.62.0 app's control-plane origin is `https://api.openbot.run`; a
   local or self-hosted server uses its own configured public origin.
2. **Desktop Usage page** — OpenBot.app 0.62.0 class: left rail **More** (`…`) > **Usage**
   (`用量` in a Chinese UI). It is a current, read-only local host report with period and agent
   filters, estimated USD cost, token totals, sessions, messages, and model/agent/day
   breakdowns. It is not the organization API and it does not show credits or budgets.
3. **Owner-supplied export** — a file or CSV the owner already has. Record its source and
   columns; do not guess missing fields.

If no surface is available, say exactly what is missing (no server origin, no owner token, no
`Usage.read` / `Budget.read`, no Usage page, no export) and stop. Do not invent a number.

## 2. Take one current report

Use a supported tool, API call, or the visible page. Take **one** snapshot for the requested
period. Do not create a routine, a watcher, or a daily snapshot. A refresh is a new
owner-requested read.

API shape, for reference:

```sh
# Token and cost summary. Never print the token.
curl -sS -H "Authorization: Bearer $OPENBOT_TOKEN" \
  "$OPENBOT_API_BASE/v1/organization/usage?from=$FROM&to=$TO&groupBy=bot"
```

Use `groupBy=bot` to rank bots, `groupBy=source` for activity, and `groupBy=day` for day
trends. Keep the response's `from`, `to`, `groupBy`, `total`, and `items[]` together. `key` can
be `null`; keep that bucket as unassigned.

## 3. Record the envelope before showing values

Write down all of these with the snapshot:

- **Source** — which API route, which desktop page, or which owner export; hosted or
  self-hosted.
- **Retrieval time** — in the owner's timezone, with the zone named (for example
  `<YYYY-MM-DD HH:MM> <IANA zone>`).
- **Reporting period** — explicit start and end, and whether it is a trailing window or a
  fixed calendar window.
- **Source timezone** — API defaults are UTC; the desktop page uses the host IANA zone; an
  export's zone may be different.
- **Units and denominators** — token counts, `costMicros` (micro-USD; 1 USD = 1,000,000
  micro-USD), estimated USD, sessions, calls, or shares of known amounts.
- **Grouping and filters** — `groupBy`, agent filter, metric filter, and the period control.
- **Completeness** — `pendingCalls`, `unknownCalls`, partial-data warnings, unavailable
  fields, and every `null`. Null stays unknown; never replace it with zero.
- **Scope** — organization usage, a bot/member/token slice, a credit balance, or a budget.
  Keep these distinct.

## 4. Hand off

- Give the snapshot to `usage-visibility-dashboard`. Keep quota, bot ranking, activity, and
  day trend views separate; do not invent a joint bot-by-activity table from marginal totals.
- For `usage-optimization-impact-report`, compare only the same source, same metric, and same
  window type. Record the baseline and the later read; report observed change in the source's
  units, never "saved N tokens" or a calculated dollar saving.
- For OpenBot `groupBy=source`, use `turn`, `compaction`, `judge`, `bot_memory`, and `other`.
  Do not relabel them as another product's chat / routine / bot-to-bot categories.
- Label the desktop page's USD figure as an API-equivalent estimate, not a subscription charge
  or an organization invoice.

## 5. Security and failure

Never print, copy, or extract a token, cookie, or session. Never read `openbot.db` for a
credential and never write to it. Never use a budget/credit write or delete route. If the read
fails, report the missing surface or permission exactly; do not fill the dashboard with
fabricated data.

See `adapters/openbot.md` for the full contract and official links.
