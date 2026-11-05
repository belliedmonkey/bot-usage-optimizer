# Bot Usage Optimizer

A **general checker** for agent/bot products: Grok Bot and common open-source bot stacks. It turns hard-won usage waste patterns into portable check skills and a system prompt you can drop into your own auditor bot.

## Positioning

- **Product-neutral tripwires** — routines that idle or over-poll, oversized single chats, multi-bot / multi-agent overlap, bot vs local harness routing, open-bot issue handoff
- **Platform adapters** — how you pull live usage numbers differs by product; Grok Bot’s subscription usage report is one adapter example
- **Safe by default** — never invent figures; propose ≤3 changes; change only after the owner says yes; prefer pause over delete

## Checks

1. Idle / over-polled routines — `skills/usage-routine-idle-check`
2. Oversized single chats — `skills/usage-oversized-chat-check`
3. Multi-bot / multi-agent overlap — `skills/usage-multi-bot-overlap-check`
4. Bot vs local harness — `skills/usage-bot-vs-harness-check` (console/SaaS work stays on the bot; local heavy coding goes to a harness)
5. Open-bot issue handoff — `skills/usage-open-bot-handoff-check` (premium seat files issues; cheaper open seats execute)

## Contents

| Path | Role |
|------|------|
| `prompt/system.md` | Auditor bot system prompt |
| `skills/*/SKILL.md` | Checklist skills |
| `skills/getting-started/SKILL.md` | First-run for a new owner |

## How to use

1. Create an auditor bot on your platform (Grok Bot, OpenBot, or another open stack).
2. Paste `prompt/system.md` into its standing instructions.
3. Install the check skills (and getting-started).
4. Wire a **usage adapter** for your platform (live usage/API or export). Without numbers, the bot must refuse to invent them.
5. Ask for an audit of routines, oversized chats, multi-bot overlap, bot vs harness routing, or open-bot issue handoff.

## License

MIT
