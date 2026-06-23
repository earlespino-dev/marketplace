# Reading HTC legs and translating them into training priorities

This guide explains how to read leg data and turn it into training focus. It is not a list of
any one runner's legs — that's runner-specific and lives in the runner's vault config.

## Where the data is

- **All 36 legs at a glance:** `${CLAUDE_PLUGIN_ROOT}/references/leg-data.md` (mileage,
  difficulty, gain/loss, net, terrain).
- **Full detail (exchange map, GPS, turn-by-turn, provisions, parking):** the leg's page in
  `${CLAUDE_PLUGIN_ROOT}/references/2026-HTC-Handbook.pdf` (pages 37–77).

Earlier HTC seasons required fetching per-leg PDFs from hoodtocoast.com. This plugin bundles the
2026 handbook, so read from the bundled file instead of the website. If asked about a different
year, confirm whether the course changed and fall back to the live course-maps page only then.

## Fields that matter on each leg

- **Distance** (miles).
- **Difficulty:** E / M / H / VH (official rating).
- **Elevation gain / loss** (e.g. `912 / -322 ft`) and **net** (gain minus loss). Both numbers
  matter: a leg can net downhill while still having real climbs, or vice versa.
- **Terrain / surface:** paved vs. gravel vs. trail, shoulder width, hazard callouts.
- **Time-of-day:** any leg run 6:00pm–7:00am needs reflective vest + front/back LED flashers +
  flashlight/headlamp (vest until 9:00am). Whether a given leg is "at night" depends on the
  team's start time, not the leg number.

## Worked example (format reference)

Leg 8 reads: `6.00 Mi | Moderate · 140 / -346 ft · net -206 ft · downhill and rolling country
roads, limited paved shoulder`. From this: it's net downhill with modest swings → the priority
is downhill rhythm and quad durability, not climbing — despite the unremarkable "moderate" label.

Contrast leg 20: `5.58 Mi | Very Hard · 912 / -322 ft · net +590 ft · gravel backcountry,
partially paved`. Big sustained climb on uneven gravel → hill strength + footing + (likely)
low-light comfort. This is usually the leg to build the week around if a runner has it.

## Across a runner's three legs

- **Steepest/longest climb** → highest-leverage leg to train specifically (hill repeats,
  climbing strength).
- **Biggest net downhill / steepest descents** → downhill-specific running (controlled fast
  descending, eccentric quad tolerance) — not just "the easy leg."
- **Last leg in the rotation** → run on accumulated fatigue and disrupted sleep; train executing
  while tired regardless of that leg's own rating.
- **Any night leg** → at least occasional low-light/evening training, even if home terrain
  differs from race terrain.
