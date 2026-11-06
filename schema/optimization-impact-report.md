# Optimization impact report — empty schema

Copy these fields when storing an accepted optimization. Do not fill them with sample people, bot names, or usage numbers in public templates.

| Field | Meaning |
| --- | --- |
| `recordedAt` | When the owner-approved change happened |
| `timezone` | Owner timezone label for displayed times |
| `check` | Check that found it, or `owner-requested` |
| `target` | Named bot, routine, chat pattern, or other object |
| `action` | What changed |
| `expectedMechanism` | Why this might reduce waste, in plain words |
| `measurementStatus` | `observing`, `compared`, or `unmeasurable` |
| `baseline.source` | Usage report or adapter used |
| `baseline.retrievedAt` | When the baseline snapshot was read |
| `baseline.period` | Reporting window |
| `baseline.sourceTimezone` | Timezone of the source report |
| `baseline.units` | Units as the source reports them |
| `baseline.denominators` | What each figure is a share or portion of |
| `comparison` | Same-source, same-metric, same-window-type follow-up; or unknown |
| `comparison.metric` | Exact metric compared |
| `comparison.before` | Baseline value in that metric |
| `comparison.after` | Later value in that metric |
| `comparison.notes` | Including that shares are relative to all usage in the window |
| `observedSpend` | Only if the source itself reported money, with that source's scope; otherwise omit |

Never convert shares or quota percentages into tokens. Never invent a dollar saving. Missing values stay unknown, never zero.
