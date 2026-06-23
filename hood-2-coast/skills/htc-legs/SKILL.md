---
name: htc-legs
description: Look up the profile of any Hood to Coast / Portland to Coast leg — distance, difficulty rating, elevation gain/loss and net, terrain/surface, gravel and night-leg flags, exchange details, GPS, and turn-by-turn directions. Use when asked "what's leg N like", "which of my legs is hardest", "show my route/directions", "how much climbing is on leg 20", or to compare a runner's three legs. Reads the transcribed leg table and the bundled 2026 HTC Handbook. Answers any leg-by-number lookup standalone (no config needed); for the runner's OWN legs, defers to htc-setup first when no saved config exists.
---

# HTC Leg / Course Lookup

Answers questions about specific legs or the course as a whole, grounded in real handbook data
rather than memory.

## Step 0: Check for a runner config

Before answering, check whether a runner config exists at `<vault_path>/htc-trainer-config.md`
(if you don't know the runner's vault path, that itself signals setup hasn't run yet).

- If the request is about **the runner's own legs** ("my legs," "my hardest leg," "my route")
  and **no config exists**, run **htc-setup** first so you actually know their runner number,
  team size, and three legs — then resume here. Don't guess which legs are theirs.
- If it's a **generic/public lookup** (any leg by number, "what's leg 20 like," comparing
  arbitrary legs), answer standalone from the data sources below — no config needed — but
  mention once that running **htc-setup** personalizes this and unlocks the training and packing
  skills.

## Data sources (in order)

1. **`${CLAUDE_PLUGIN_ROOT}/references/leg-data.md`** — fast table of all 36 legs: mileage,
   difficulty (E/M/H/VH), gain/loss, net elevation, terrain summary, and gravel/night notes.
   Use this for most questions.
2. **`${CLAUDE_PLUGIN_ROOT}/references/2026-HTC-Handbook.pdf`** (leg pages 37–77) — authoritative
   for the full exchange map, GPS coordinates, exact turn-by-turn directions, parking,
   provisions, and "vans may not stop" callouts. Read the relevant page when the runner needs
   any of that.

## Which legs are a runner's?

If a config exists (`<vault_path>/htc-trainer-config.md`), default to that runner's three legs
when they ask about "my legs." Otherwise derive from runner number + team size:

- **12-person:** runner N → legs N, N+12, N+24.
- **8/10-person:** use the rotation table (handbook p.16) — see htc-logistics.

## Interpreting a leg (what to tell the runner)

- **Net vs. swings:** report both gain and loss, not just the label. A "moderate" leg can hide
  steep descents (e.g. leg 8 nets -206 ft but is downhill+rolling). The swings inside the net
  drive the training need.
- **Downhill legs** (big net loss / steep descents — legs 1, 2, 3, 30, 36): training need is
  controlled fast descending and quad durability, not climbing.
- **Climb legs** (big net gain — legs 20, 18, 5, 35, 29): hill strength, and uneven-footing
  comfort if gravel (leg 20).
- **Night legs:** which legs fall in the 6:00pm–7:00am window depends on the team's start time,
  not the leg number — compute from the schedule (htc-logistics), then flag required reflective
  gear (htc-rules).
- **Gravel/dust:** legs 20, 21 (bandana recommended), plus gravel stretches on 35 and 36.

## Comparing a runner's three legs

Look at the three together: which has the steepest sustained climb (highest-leverage to train),
which has the biggest descent (downhill-specific work), and which falls last in their rotation
(run on accumulated fatigue regardless of its own difficulty). See `references/leg-reading-guide.md`
for the full translation from leg profile to training priority — read it the first time you
analyze a runner's set of legs.
