# Bot Usage Optimizer

A **general checker** for agent/bot products: Grok Bot and common open-source bot stacks. It turns hard-won usage waste patterns into portable check skills and a system prompt you can drop into your own auditor bot.

## Positioning

- **Product-neutral tripwires** — idle/over-polled routines, oversized chats, multi-bot overlap, bot vs local harness, open-bot issue handoff, skill gaps, paste bridges, script vs chat (incl. lightest supported tool), failure retry limits
- **On-demand visibility** — presentation capability for usage by bot and activity; high usage alone does not prove waste; **no usage-dashboard polling**
- **Optional memory slimming** — maintenance capability, **default OFF**; schedule enablement and memory-deletion permission are separate; not a waste tripwire; not usage polling
- **Platform adapters** — how you pull live usage numbers differs by product; Grok Bot’s subscription usage report is one adapter example
- **Safe by default** — never invent figures; propose ≤3 changes; change only after the owner says yes; prefer pause over delete

## Checks (9 tripwires)

1. Idle / over-polled / unfiltered routines — `skills/usage-routine-idle-check`
2. Oversized single chats — `skills/usage-oversized-chat-check`
3. Multi-bot / multi-agent overlap (incl. few good seats) — `skills/usage-multi-bot-overlap-check`
4. Bot vs local harness — `skills/usage-bot-vs-harness-check`
5. Open-bot issue handoff — `skills/usage-open-bot-handoff-check`
6. Skill gaps — `skills/usage-skill-gap-check`
7. Manual paste bridges — `skills/usage-manual-bridge-check`
8. Script vs chat — `skills/usage-script-vs-chat-check` (incl. lightest supported execution tool)
9. Failure retry limits — `skills/usage-retry-limit-check` (default ≤3 total failed attempts per concrete step)

## Other capabilities (not tripwires)

- Usage visibility dashboard — `skills/usage-visibility-dashboard` (on-demand; no polling)
- Optional memory slimming — `skills/usage-memory-slimming` + disabled recipe `routines/weekly-memory-slimming.md` (default OFF; review-only until scoped write-back is separately authorized)

## Contents

| Path | Role |
|------|------|
| `prompt/system.md` | Auditor bot system prompt |
| `skills/*/SKILL.md` | 9 checks + visibility + memory slimming + onboarding (**12 skills**) |
| `skills/getting-started/SKILL.md` | First-run (Grok alias: `bot-usage-getting-started`) |
| `routines/weekly-memory-slimming.md` | **Disabled** weekly recipe (docs only; not an active routine) |

## How to use

1. Create an auditor bot on your platform (Grok Bot, OpenBot, or another open stack).
2. Paste `prompt/system.md` into standing instructions, **or** install an included onboarding skill that embeds them. Do not rely only on workspace-only files Marketplace may omit.
3. Install the twelve skills listed above. Do **not** treat the weekly memory recipe as auto-enabled.
4. Wire a **usage adapter**. Without numbers, refuse to invent them.
5. Ask for visibility, an audit among the nine tripwires, or (only if desired) opt into memory slimming with separate schedule + deletion decisions.

Public links: [GitHub repo](https://github.com/belliedmonkey/bot-usage-optimizer) · [Grok Bot template](https://x.ai/bot/mhUDyoBQmdRT8MIFjAmXD)

## License

MIT
