# Bot Usage Optimizer

A **general checker** for agent/bot products: Grok Bot and common open-source bot stacks. It turns hard-won usage waste patterns into portable check skills and a system prompt you can drop into your own auditor bot.

## Positioning

- **Product-neutral tripwires** — idle/over-polled routines, oversized chats, multi-bot overlap, bot vs local harness, open-bot issue handoff, skill gaps, paste bridges, script vs chat (incl. lightest supported tool), failure retry limits
- **On-demand visibility** — a separate presentation capability that makes usage understandable by bot and activity before any cut suggestion; high usage alone does not prove waste
- **Platform adapters** — how you pull live usage numbers differs by product; Grok Bot’s subscription usage report is one adapter example
- **Safe by default** — never invent figures; propose ≤3 changes; change only after the owner says yes; prefer pause over delete; never install polling or a seat just to refresh a dashboard

## Checks (9 tripwires)

1. Idle / over-polled / unfiltered routines — `skills/usage-routine-idle-check`
2. Oversized single chats — `skills/usage-oversized-chat-check`
3. Multi-bot / multi-agent overlap (incl. few good seats) — `skills/usage-multi-bot-overlap-check`
4. Bot vs local harness — `skills/usage-bot-vs-harness-check` (console/SaaS work stays on the bot; local heavy coding goes to a harness)
5. Open-bot issue handoff — `skills/usage-open-bot-handoff-check` (premium seat files issues; cheaper open seats execute)
6. Skill gaps — `skills/usage-skill-gap-check` (re-teaching → write a skill)
7. Manual paste bridges — `skills/usage-manual-bridge-check` (connectors/vault close the loop)
8. Script vs chat — `skills/usage-script-vs-chat-check` (deterministic workflows → scripts + thin skills; prefer the lightest supported execution tool)
9. Failure retry limits — `skills/usage-retry-limit-check` (default ≤3 total failed attempts per concrete step; stricter auth/approval/service rules win; no fresh unlimited budget on each routine wake)

## Presentation capability (not a tripwire)

- Usage visibility dashboard — `skills/usage-visibility-dashboard`

Shows quota/reset (when present), bots ranked by the report’s metric and period, and chats / routines / bot-to-bot when the source supplies those categories. Label every figure with source, retrieval time, reporting period, units, and denominators. Never infer a bot-by-activity joint from two separate marginal totals; omit flow/stacked joint views unless real joint values exist. Snapshot only—refresh needs a new owner-requested source read.

## Contents

| Path | Role |
|------|------|
| `prompt/system.md` | Auditor bot system prompt |
| `skills/*/SKILL.md` | 9 check skills + visibility + onboarding (11 skills) |
| `skills/getting-started/SKILL.md` | First-run for a new owner (Grok template alias: `bot-usage-getting-started`) |

## How to use

1. Create an auditor bot on your platform (Grok Bot, OpenBot, or another open stack).
2. Paste `prompt/system.md` into its standing instructions, **or** install an included onboarding/system skill that already embeds those instructions. Do not rely only on workspace-only files that Marketplace packages may omit.
3. Install the nine check skills, `usage-visibility-dashboard`, and getting-started.
4. Wire a **usage adapter** for your platform (live usage/API or export). Without numbers, the bot must refuse to invent them.
5. Ask for a **usage visibility** snapshot first when you want the picture clear, then pick an audit among the nine tripwires.

Public links: [GitHub repo](https://github.com/belliedmonkey/bot-usage-optimizer) · [Grok Bot template](https://x.ai/bot/mhUDyoBQmdRT8MIFjAmXD)

## License

MIT
