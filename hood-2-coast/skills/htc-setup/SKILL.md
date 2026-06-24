---
name: htc-setup
description: One-time setup and ongoing maintenance of a Hood to Coast / Portland to Coast runner's profile — runner number, team size, location, race date, Obsidian vault path, derived three legs, and optional shoe rotation. Saves a config the other HTC skills (htc-trainer, htc-legs, htc-packing) read on every run. Use the first time anyone asks about their HTC/PTC training, legs, or packing and no config exists yet, or whenever the runner needs to change saved details (moved, new race date, new runner number, new shoes). Also use to re-derive legs from a runner number or to set up a different runner on a shared device.
---

# HTC Runner Setup

Establishes and maintains the per-runner config that every other skill in this plugin depends
on. This is the single source of truth for who the runner is, where they are, and which three
legs they run. Keep it accurate; the training plan is only as good as this file.

## When to run

- A runner asks anything HTC/PTC-related (today's run, their legs, packing) and **no config
  file exists yet** in their vault → run full setup, then hand back to the skill they wanted.
- The runner says something that contradicts the saved config (moved, race date changed, new
  shoes, different runner number) → update the existing file, don't just use it for one turn.
- Someone on a shared device whose saved config clearly belongs to a different person → offer
  to set up a fresh config rather than applying someone else's.

## Where the config lives

```
<vault_path>/htc-trainer-config.md
```

One file per runner, inside that runner's own Obsidian vault — not inside this plugin. That's
what keeps the plugin reusable across different people. Use
`${CLAUDE_PLUGIN_ROOT}/skills/htc-setup/assets/config-template.md` as the structure (YAML
frontmatter + body). Always read this file at the start of any HTC task; treat it as
authoritative.

## Setup interview (ask all at once, accept reasonable defaults)

1. **Runner number** (1–12) — determines the three legs.
2. **Team size** (8, 10, or 12) — needed to derive legs correctly. **Don't assume 12.**
3. **Location** for weather (city/state, or lat/long).
4. **Race date** — Hood to Coast is the last weekend of August; confirm the exact date for the
   year in question via web search, since it shifts year to year. Also ask the runner's
   flight/travel-out date if relevant — it ends the training window before race day.
5. **Obsidian vault path** — absolute filesystem path where notes get written. This only works
   in an environment with access to the runner's filesystem (Claude Code or Desktop locally);
   say so plainly if that's not the case.
6. **Shoe rotation** (optional) — only if they want shoe recommendations. If yes, get each shoe
   and its role (daily trainer, tempo, trail/gravel, race day). Skip entirely if they decline.
7. **Preferred running times** (optional) — ask two separate questions so htc-trainer can time
   its recommendations around the runner's life:
   - *"When do you usually run on **weekdays**?"* — the window that fits around their work
     schedule (e.g. early morning before work, lunch, after-work evening).
   - *"When do you usually run on **weekends**?"* — the window that fits their weekend plans
     (e.g. mid-morning, flexible).
   Accept free-form answers; either can be left blank. Skip the whole item if they don't care.

## Deriving the three legs

**12-person team:** runner N runs legs **N, N+12, N+24** (runner 8 → 8, 20, 32).

**8- or 10-person team:** the simple formula breaks — use the rotation table in the handbook
(`${CLAUDE_PLUGIN_ROOT}/references/2026-HTC-Handbook.pdf`, p.16). Runners rotate through all
36 legs in order, wrapping by team size, so e.g. on a 10-person team runner 1 runs legs 1, 11,
21, 31. Confirm against the team's actual assignment — some teams deviate.

Portland to Coast (walk) uses the same leg numbering, just starting from leg 13.

After deriving the legs, pull each one's profile from
`${CLAUDE_PLUGIN_ROOT}/references/leg-data.md` (mileage, difficulty, gain/loss, net, terrain)
and save it into the config so downstream skills don't have to re-fetch it. For full
exchange/GPS/directions detail, the handbook leg pages (37–77) are authoritative.

## Writing the config

1. Fill the template with the gathered answers + the three derived legs and their pulled data.
2. Write it to `<vault_path>/htc-trainer-config.md`. If the write fails (no filesystem access),
   say so and show the content inline instead.
3. Confirm back in plain language: their three legs (with the standout one called out), the
   race countdown in weeks, and where the config was saved — before handing off to the next
   skill.

## Maintenance

When anything changes, edit the existing config file rather than creating a second one. If the
runner number or team size changes, re-derive the legs and re-pull their data.
