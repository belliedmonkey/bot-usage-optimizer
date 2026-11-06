# OpenBot usage adapter

Read-only adapter for OpenBot usage. It explains where a stable read comes from, what the
numbers mean, and how to hand one snapshot to `usage-visibility-dashboard` or
`usage-optimization-impact-report`. It is not a waste tripwire. It does not schedule or poll.

## Supported read surfaces

### 1. Organization API (documented)

The OpenBot server exposes these read routes:

| Route | What it returns | Permission |
|-------|-----------------|------------|
| `GET /v1/organization/usage` | Aggregated token counts and cost for a period, grouped by day, model, provider, member, bot, token, or source | `read` on `Usage` |
| `GET /v1/organization/usage/events` | Single model-call events, newest first, with paging | `read` on `Usage` |
| `GET /v1/organization/credits` | `enabled`, `balanceMicros`, and recent grants | `read` on `Usage` |
| `GET /v1/organization/budgets` | Budgets with their current spend | `read` on `Budget` |
| `GET /v1/organization/budgets/:budgetId` | One budget | `read` on `Budget` |

Use the origin of the OpenBot server you audit. The official docs use `api.example.com` only as
a placeholder; never copy it as a real host. The 0.62.0 desktop app's hosted control-plane
origin is `https://api.openbot.run`, but a local or self-hosted OpenBot uses its own configured
public origin. If the origin is unknown, stop and ask; do not guess a hostname.

Auth is an owner-supplied Bearer token (`Authorization: Bearer $OPENBOT_TOKEN`) or a verified
session. The documented routes are for organization administrators; the built-in `auditor` and
`administrator_read_only` roles also carry read on `Usage` and `Budget`. A personal space has a
separate wallet/credits path under `Wallet.read`; do not treat personal wallet data as
organization usage, and do not reuse an organization credit balance as a personal wallet.

Never extract a token, cookie, or session from the desktop app, the keychain, browser storage,
or `openbot.db`. Never write to `openbot.db`. Never use a budget/credit write or delete route in
a usage read.

#### `GET /v1/organization/usage`

Query:

- `from`, `to` — ISO 8601 times. Default `from` is the start of the current month in UTC;
  default `to` is now. A time without a zone is UTC.
- `groupBy` — `day` (default), `model`, `provider`, `member`, `bot`, `token`, or `source`.

Response:

- `from`, `to`, `groupBy`, `total`, `items[]`.
- Counts include `calls`, `pendingCalls`, `unknownCalls`, `inputUncached`, `inputCacheRead`,
  `inputCacheWrite`, `outputText`, `outputReasoning`, and `costMicros`.
- `items[].key` is the group value and can be `null` — for example, a call with no Bot.

#### `GET /v1/organization/usage/events`

Lists single model-call events, newest first. Query:

- `from`, `to`
- `limit` — 1 to 200, default 50
- `after` — send the previous page's `next` value to get the next page

Each event has an `id`, a `source`, a `status`, and `priced` / `charged` flags. `source` is one
of `turn`, `compaction`, `judge`, `bot_memory`, or `other`. `status` is `pending`, `confirmed`,
or `unknown`. Unknown token counts and cost are `null`, not zero.

#### Credits and budgets

`GET /v1/organization/credits` shows `enabled`, `balanceMicros`, and the newest 50 grants. It
needs `read` on `Usage`.

`GET /v1/organization/budgets` reads budgets. A budget has a `scope` (`organization`, `member`,
`bot`, or `token`), a `period` (`day` or `month`; both start at midnight UTC), a `mode` (`hard`
or `soft`), `limitMicros`, `spentMicros`, `exceeded`, `periodStart`, and a `version`. Budgets
need `read` on `Budget`.

### 2. Desktop Usage page (verified, 0.62.0 class)

OpenBot.app 0.62.0 has a read-only Usage page:

- Open the left rail's **More** (`…`) menu and choose **Usage** (Chinese UI: **用量**). On this
  build the page is not pinned to the rail by default.
- The page shows a current snapshot for the selected period, with filters for all agents,
  cost/tokens, and the period (7 days, 30 days, 90 days, or 1 year; 30 days is the default).
- It shows API-equivalent estimated cost in USD, sessions, user and assistant message counts,
  and token totals: processed without cache reads, processed with cache reads, cached input,
  uncached input, cache write, and output. It also breaks down by model, agent, and day.
- A partial-data notice reports missing usage records, records without a cost estimate, and
  incomplete token records. Unavailable values stay unavailable rather than becoming zero.
- The footer reports when collection started and when it last updated. **About these estimates**
  says the cost is API-equivalent token cost in USD, an estimate rather than a subscription
  charge; separate tool and media fees are not calculated; unknown prices and incomplete usage
  stay unavailable; shares use known amounts only and partial data can understate totals.
- Period: the trailing N local calendar days, including today, where N is the selected period.
  Time zone: the host's IANA zone, which the app passes to the report. The page does not print
  the zone, so label it from the host. On the verification host it was `Asia/Shanghai`.
- This page is **local host analytics**, not the organization API. It does not expose
  `credits.balanceMicros` or organization budgets, and its top plan rings are provider plan
  windows, not OpenBot credits.

### 3. Agent tool

No built-in `usage.getUsage`, `usage.listUsageEvents`, or `usage.getCredits` tool was verified.
The official "OpenBot gives every Bot these tools" list covers bot listing, bot details,
delegation, delegation cancellation, and bot creation; it has no usage tool. The 0.62.0 app's
tool strings showed no usage tool either. Do not tell a bot to call one unless the host has
installed and tested such a tool. The documented read path is the HTTP API; the desktop page is
a human-facing read.

## Periods and time zones

- API: the defaults and any timestamp without an offset are **UTC**. The API has no separate
  display-timezone parameter; pass explicit `from` / `to` values with `Z` or an offset.
- Budget periods: `day` and `month` both start at midnight **UTC**.
- Desktop page: trailing local calendar days in the host IANA zone. Record the zone; do not
  assume it is UTC or assume the API's UTC window matches the page's local window.
- `groupBy=day` keys are source day labels. Do not merge them with local-day buckets from the
  desktop page or from another product without restating the conversion.

## Units and denominators

- Token counts are counts, not rates. `inputCacheRead` is a repeated read of cached context,
  not extra input on top of `inputUncached`; do not add the two and call the result "processed
  tokens" unless the source itself does that.
- `costMicros` is **micro-USD**: 1 US dollar = 1,000,000 micro-USD.
  `USD = costMicros / 1,000,000`. Do not round a non-zero micro amount down to zero; state
  micro-USD or show enough decimal places.
- The desktop page's `estimatedCostUsd` is a USD estimate from host records, not an API
  `costMicros` value. Do not present it as an organization invoice or convert it back into an
  API field.
- A share needs its denominator. State whether a share is of known cost, known tokens, all
  sessions, or all calls, and state the period. A share of known amounts is not a share of the
  plan limit.
- Keep confirmed, `pendingCalls`, and `unknownCalls` separate. Preserve `null` as unknown,
  never zero. Unknown usage can keep a budget hold even though no confirmed cost was recorded.

## Mapping onto visibility views

| Visibility view | OpenBot source | Rule |
|-----------------|----------------|------|
| Quota | `credits.balanceMicros`; budget `limitMicros` / `spentMicros` / `exceeded` / `periodStart` | Keep credit balance and budget cap distinct. Show scope and period. Never sum a credit balance and a budget limit, and never call a budget a wallet. |
| Rank bots | `groupBy=bot` | Group by the API `bot` key. `items[].key` may be `null`; keep a "No bot / unassigned" bucket instead of dropping or zeroing it. |
| Activity | `groupBy=source`, or event `source` | Use the documented labels `turn`, `compaction`, `judge`, `bot_memory`, `other`. Do **not** relabel them as Grok Bot's chat / routine / bot-to-bot categories. The desktop page has no source breakdown; do not invent one from its agent/model/day tabs. |
| Day trends | `groupBy=day` | Compare only compatible windows and metrics. Label the source timezone. |
| Event detail | `/v1/organization/usage/events` | Use for per-call detail and `pending` / `unknown` examples. Do not use a partial event page as the denominator for a period total. |

For the desktop page, the agent breakdown is a host-side agent label, not necessarily an API
`bot` row. Keep the label as "agent" unless the API's `bot` key is what produced it.

## Failure and privacy rules

- If there is no server origin, no owner-supplied token, no `Usage.read` / `Budget.read`
  permission, no verified Usage page, or no owner export, say exactly what is missing. Do not
  fill the gap with estimates.
- If a surface exists but is partial, keep its partial-data warning and leave unavailable
  values unavailable. Do not reconcile a partial total with a different source.
- Never invent token or cost figures, savings, reset times, or private links.
- Do not install polling, a watcher, a daily snapshot, or a new seat to refresh usage. A refresh
  is a new owner-requested read.
- Do not put personal bot names, agent names, usage snapshots, private links, or credentials
  into a public template or repository.

## Verification status

- Official docs re-checked 2026-11-06: [Usage and budgets](https://docs.openbot.build/usage/),
  [usage.getUsage](https://docs.openbot.build/api/operations/usagegetusage/),
  [usage.listUsageEvents](https://docs.openbot.build/api/operations/usagelistusageevents/),
  [usage.getCredits](https://docs.openbot.build/api/operations/usagegetcredits/),
  [budgets.getBudget](https://docs.openbot.build/api/operations/budgetsgetbudget/).
- Desktop Usage page verified in OpenBot.app 0.62.0 on macOS. No personal values are recorded
  here.
- Organization API read was not performed in that environment: no owner-supplied
  `OPENBOT_TOKEN` or verified organization-admin session was present, and the desktop page is
  local host analytics rather than the organization API. A working desktop page does not prove
  that `Usage.read` is available on the server.
- No built-in usage agent tool was found in the official every-Bot tool list or the 0.62.0 app.

## Official links

- <https://docs.openbot.build/usage/>
- <https://docs.openbot.build/api/operations/usagegetusage/>
- <https://docs.openbot.build/api/operations/usagelistusageevents/>
- <https://docs.openbot.build/api/operations/usagegetcredits/>
- <https://docs.openbot.build/api/operations/budgetsgetbudget/>
- <https://docs.openbot.build/delegation/>
