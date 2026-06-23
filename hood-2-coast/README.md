# hood-2-coast

A [Claude Code](https://claude.com/claude-code) plugin for training for and running the
**Hood To Coast / Portland To Coast** relay. Everything is grounded in the bundled 2026 HTC
Handbook and a config saved in your own Obsidian vault, so it works for any runner on any team.

## Skills

| Skill | What it does |
|---|---|
| **htc-setup** | One-time profile setup + maintenance (runner number, team size, location, race date, vault path, your three legs, optional shoes). Owns the per-runner config the other skills read. |
| **htc-trainer** | Daily/weekly training plan tuned to your legs, weather, recent training load, and weeks-to-race phase. Writes a dated note into your vault. |
| **htc-legs** | Look up any leg's profile — distance, difficulty, elevation, terrain, gravel/night flags, directions. |
| **htc-packing** | Personalized packing list tuned to your legs, night gear, and weather. |
| **htc-rules** | Authoritative race rules, penalties, required safety gear, volunteer rules, Cut & Run. |
| **htc-logistics** | Team & van planning — rotation, drivers, schedule, safe houses, volunteers, spectating. Owns a per-team config. |

## Getting started

1. **Install** (if you haven't already):
   ```sh
   claude plugin marketplace add /Users/earlespino/projects/marketplace
   claude plugin install hood-2-coast@earl-marketplace
   ```
2. **Run setup first.** The first time you ask anything about your training, legs, or packing,
   the plugin runs **htc-setup** to capture your runner number, team size, location, race date,
   and Obsidian vault path, and derives your three legs. Everything else reads that config.
   - Vault writes only work where Claude can reach your filesystem (Claude Code or Claude
     Desktop running locally).
3. **Then just ask** — "what should I run today?", "what's leg 20 like?", "what do I pack?",
   "how do the vans rotate?" — and the matching skill fires.

## Optional: connect the Strava MCP (recommended for training plans)

**htc-trainer** produces a much sharper plan when it can see your *actual* recent training —
mileage, intensity, fatigue, layoffs — which it reads from your Strava history via the official
**Strava MCP server**.

This is **optional**. Without it, the trainer still builds a plan from weather, your legs'
terrain, and your weeks-to-race phase — it just can't factor in your real training load, and
will say so in the note.

### Set it up

1. Add the Strava MCP server (HTTP transport):
   ```sh
   claude mcp add --transport http strava https://mcp.strava.com/mcp
   ```
   - Add `--scope user` to make it available in every project; omit it to scope to the current
     project only (the default).

2. Authenticate with Strava. In Claude Code, run:
   ```
   /mcp
   ```
   then select **strava** and complete the Strava OAuth login in your browser. (The first
   connection will prompt you to authorize access to your activities.)

3. Verify the connection:
   ```sh
   claude mcp list
   ```
   You should see `strava: https://mcp.strava.com/mcp (HTTP) - ✔ Connected`.

That's all — htc-trainer will automatically use it on the next training-plan request. To remove
it later: `claude mcp remove strava` (add `-s user` if you added it at user scope).

> Note: connecting an MCP server is a Claude Code configuration step, not something the plugin's
> skills can do for you — so this one-time setup is on you. The skills will use Strava if it's
> connected and degrade gracefully if it isn't.

## Weather

htc-trainer and htc-packing use current weather for your saved location. No extra setup is
required beyond having setup save your location.

## Updating / hacking on the plugin

The canonical source is this directory inside the `earl-marketplace` repo. After editing a skill:

```sh
claude plugin marketplace update earl-marketplace
claude plugin update hood-2-coast@earl-marketplace
```

then restart Claude Code or run `/reload-plugins`.
