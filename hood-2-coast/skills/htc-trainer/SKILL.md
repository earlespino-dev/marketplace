---
name: htc-trainer
description: Generates a daily or weekly running training plan for Hood to Coast / Portland to Coast relay prep, tuned to the runner's assigned legs, location, and race date. Pulls current weather, reviews recent Strava training history for fatigue/volume, factors in the official terrain/elevation profile of the runner's three legs, and writes a dated training-plan note into the runner's Obsidian vault. Use whenever asked about today's or tomorrow's run, this week's training, what workout to do, logging a workout, weeks left until the race, or anything about HTC/PTC training — even without naming the skill. Reads the runner config saved by htc-setup; if no config exists yet, run htc-setup first.
---

# HTC Runner Trainer

Produces a Markdown training-plan note for a specific day (or short forward window), grounded
in three real things rather than a generic plan:

1. **Actual weather** for the runner's location.
2. **Actual recent training load** from Strava — mileage, intensity, fatigue, layoffs.
3. **The actual terrain of the runner's three assigned legs** — from the saved config / the
   bundled handbook, not guessed.

## Step 0: Read the config (and bail to setup if missing)

Read `<vault_path>/htc-trainer-config.md`. If no config exists, invoke **htc-setup** first,
then resume here. If the runner says anything that contradicts the config (moved, new shoes,
race date changed), update it via htc-setup rather than using the new info for just this run.

## Step 1: Timeframe

Default to **today**, unless the user says otherwise ("tomorrow," "this week," "Saturday's
run"). For a multi-day window, write **one note per day**, each following the same structure.

## Step 2: Weather

Fetch current conditions for the runner's saved location (or wherever they specify if
traveling). Weather changes the plan for concrete reasons:

- Heat/humidity should shorten or de-intensify a hard hill session — heat compounds hill load.
- If the runner's hardest leg will be run at night (see the config / htc-legs), note when
  current training conditions diverge (training in daylight for a night leg) and suggest
  occasional condition-matched sessions.
- Rain/wet is a chance to practice footing if any leg involves gravel or trail (legs 20, 21,
  35, 36).
- Wind, temperature swings, and daylight window shift whether the run happens AM/midday/evening.

**When to run (use the runner's saved preference as the default).** If the config tracks run
times (`tracks_run_times: true`), default the suggested time to the runner's **weekday** window
for a Mon–Fri plan or their **weekend** window for a Sat–Sun plan — so the recommendation fits
around their work schedule or weekend plans — and state that time in the plan. Treat it as a
**soft default**: weather safety (heat advisory, storms) and leg-specificity (an occasional
condition-matched night/low-light session for a night leg) can override it, but say so in one
line when you diverge (e.g. "shifted earlier than your usual evening run because of the heat").
If run times aren't tracked, choose the window from weather/daylight as usual.

Late-August Oregon priors worth knowing: rain is usually low (a passing sprinkle at most), but
heat is highly variable — recent years have ranged from a wet weekend to the hottest on record
(low 100s midday). Watch the actual forecast in the weeks before the race.

## Step 3: Recent training from Strava

Use the Strava tools to understand the last 7–10 days: volume, intensity, any hill/interval
work, and whether today should be hard or easy. Synthesize into a couple of sentences — don't
dump the raw activity list ("You've run 22 mi over 6 days with one hill session Tuesday — legs
should be fresh for a harder effort today"). If Strava fails or returns nothing useful, say so
in the note and proceed on a sensible default (assume moderate fitness; ask if anything's
nagging) rather than blocking.

## Step 4: Bias toward the runner's actual limiter

Use the three legs from the config. Each has a different training job based on its real profile:

- A leg with a large **net downhill** and real elevation swings needs quad-eccentric/descending
  tolerance — fast, controlled downhill running (e.g. the Mt. Hood legs 1–3 drop 1,300–2,000 ft).
- A leg rated **hard/very hard** with significant **net climb**, especially on gravel or at
  night (e.g. leg 20: +590 ft over 912 ft of gain, gravel), is usually the highest-leverage leg
  to train for — hill strength, uneven footing, low-light comfort.
- A leg run **last in the rotation** is run on accumulated fatigue and disrupted sleep — train
  fatigue resistance and executing while tired, not just terrain.

Weight the week toward the actual limiter (usually the hardest-rated leg) while still touching
the other two. If Strava shows an imbalance (hardest leg is a climb but no hill work in weeks),
correct toward it. If the runner's home is flat and lacks their race terrain, say so and suggest
the best local substitute (parking-garage ramps, bridges, treadmill incline, nearest trail).

### Where to run (locations & routes)

When the runner asks where to run — or when today's workout needs specific terrain and you want
to point them somewhere concrete — **consult Strava first**, in this order:

1. `get_athlete_profile` → anchor on the runner's location.
2. `list_activities` with `include_polyline: true` (recent range) → find routes/spots they
   already run, so you can recommend a real, familiar route by name/landmark.
3. When the workout needs particular terrain (e.g. hills for leg 20), optionally
   `get_activity_streams` (`location`, `altitude`, `grade_smooth`) on a candidate past activity
   to confirm it matches — e.g. "your Tuesday park loop has the rolling climb you need."

Prefer recommending routes the runner has already run. Note: this uses the runner's own past
tracks + profile location — Strava's saved "Routes" and segment search aren't available on this
MCP, and reduced polylines are good for "which area/route," not turn-by-turn.

**Web fallback is on request only.** Do *not* automatically search the web for places to run. If
Strava is unavailable or its history doesn't cover what's needed, say so and *offer* a web search
for local trails/routes near their location — only run it if the runner asks for it.

### Build in real recovery — don't write a hard day every day

Check Strava for the last 2–3 days before setting today's intensity:

- If the last 1–2 days already had a hard or long effort, default today to **easy/rest**,
  regardless of the leg-focus rotation. Not stacking hard days matters more than hitting the
  perfect leg stimulus.
- Rough week shape: 1–2 quality sessions, 1–2 easy runs, ≥1 full rest/active-recovery day. More
  rest early in the buildup; the hard/easy ratio can rise slightly near race day but never
  vanish.
- A rest day still gets a short note if the runner's checking in — name it as deliberate
  recovery and suggest mobility/foam-rolling/stretching for whatever's been loaded.

Relay-specific note: the inter-leg breaks mean the runner doesn't need to train 15 continuous
miles. The specific adaptation that matters is **running on tired legs** — e.g. a 5K in the
morning, another in the evening, another the next morning — to rehearse three efforts in ~36
hours. Half-marathon fitness is a good readiness litmus test.

## Step 4.5: Shoe (only if the runner opted in)

If the config tracks shoes, match the shoe to today's workout and name it in the workout
section. Reserve a race-day-specific shoe (carbon plate) for race day, not training. If shoes
aren't tracked, skip silently.

## Step 5: Phase from weeks-out

Compute weeks remaining as `(race date − today) / 7`, rounded down, from the saved race date.

| Weeks out | Phase | Emphasis |
|---|---|---|
| 8+ | Base | Aerobic volume, intro hill strength, get comfortable with the legs' terrain, occasional condition-matched session (e.g. evening run for a night leg) |
| 4–7 | Build | Sharper hill repeats or downhill-specific work matched to the hardest leg; start stacking hard/easy/hard across 24–36 hrs to mimic the relay |
| 2–3 | Peak | Highest specificity: a session matched to the hardest leg's conditions + at least one deliberate "tired legs" run. Volume plateaus, not climbs. |
| 1 | Taper | Cut volume sharply, keep a few short sharp efforts, prioritize sleep/travel logistics — account for the travel-out date, which may shorten this week. |
| 0 (race week) | Race week | Light activity, mobility, hydration, logistics — not a training day. |

State the phase and weeks-out plainly in the note.

## Step 6: Write the plan

Use the saved vault path and the template at
`${CLAUDE_PLUGIN_ROOT}/skills/htc-trainer/assets/training-plan-template.md`. If the write fails,
say so and offer the content inline. Fill: `date` (YYYY-MM-DD), `weeks_to_race`, `phase`,
`phase_tag`, `target_leg_focus`, `weather_summary`/`weather_block`, `strava_summary`,
`workout_title`/`workout_body` (specific: distance/duration, pace/effort, terrain), `shoe`
(only if opted in), and `rationale` (2–4 sentences tying the workout to the runner's leg demands
and recent Strava). File name: `YYYY-MM-DD-training-plan.md` in the vault folder (check for a
`Daily/` subfolder before assuming flat structure).

## Step 7: Confirm

Tell the runner today's plan concisely (don't make them open Obsidian). If they're just chatting
("what should I run today") rather than asking to log it, it's fine to answer inline — only write
the note when the request implies saving, which is the default given setup; check if ambiguous.

## Edge cases

- **No Strava data:** don't block — plan from weather + leg data + phase; ask once for training
  background. For "where to run" requests with no Strava history, *offer* a web search for local
  routes rather than running one automatically (see "Where to run").
- **Injury/soreness/fatigue mentioned in the prompt:** overrides the computed phase — adjust
  down and say so. (Several teammates have run on niggles/Achilles/back issues — err cautious.)
- **Weather makes terrain work unsafe** (thunderstorms, heat advisory): substitute indoor/
  treadmill and explain the swap.
- **Race week / post-travel:** logistics and rest, not a training session.
