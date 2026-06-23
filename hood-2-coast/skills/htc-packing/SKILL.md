---
name: htc-packing
description: Produce a personalized Hood to Coast / Portland to Coast packing list — what to bring for the van, for each of the runner's three legs, for night running, and for the overnight/coast portions. Tunes the official handbook packing list to the runner's legs (e.g. bandana for dusty gravel legs), the night-gear requirements, and the expected weather. Use when asked what to pack, what to buy/bring, what gear is needed, whether to bring a sleeping bag, or to build a checklist before the race.
---

# HTC Packing List

Builds a packing list grounded in the official handbook list, then personalizes it to the
runner's legs and conditions.

## Sources

- Official packing list: `${CLAUDE_PLUGIN_ROOT}/references/2026-HTC-Handbook.pdf`, p.13.
- Required safety gear (drives the non-negotiables): see htc-rules / handbook p.9, 27.
- The runner's legs + weather: from the config (`<vault_path>/htc-trainer-config.md`) and a
  live forecast. If no config, ask runner number + team size or just give the general list.

## The baseline list (from the handbook)

**Clothing:** three sets of running clothes; running shoes + a spare pair; warm-ups; swimsuit;
running gloves; sunglasses; GPS watch. Pro tip from the handbook — pack each running outfit in
its own labeled Ziploc so you can grab the next one fast and stash the dirty one.

**Required safety (team minimum, but bring your own):** 2 reflective vests, 2 LED flashers,
2 flashlights/headlamps per team. **Every runner on course from 6:00pm–7:00am must personally
wear a reflective vest + front/back LED flasher + flashlight/headlamp** (vest until 9:00am) —
so plan to have your own, don't rely on sharing two across six people.

**Equipment:** large water jugs + reusable bottles; recycling/landfill bags; Ziplocs for wet
clothes; scotch/masking tape (team number signs on van windows — required, 60-min penalty if
not displayed).

**Toiletries:** towel/washcloth, toothbrush, antiperspirant, sunscreen, bug spray, hand
sanitizer/wipes (real showers are rare on course).

**Accessories:** earplugs (for sleeping in a moving van), first aid (blister care, Icy Hot,
aspirin, antacids, instant ice packs, Ace bandages), phone + charger, **sleeping bag + small
pillow**, food/snacks.

## Personalize it

- **Dusty/gravel legs (20, 21; gravel stretches on 35, 36):** add a **bandana/buff** to keep
  dust out — the handbook calls this out specifically for legs 20 & 21.
- **Night legs:** make sure the runner's own vest/flasher/headlamp are packed and charged; add
  spare batteries. Flag which of their legs are likely at night (depends on start time — see
  htc-logistics).
- **Hot forecast (late-Aug Oregon can hit low 100s midday):** extra electrolytes, more water,
  hat, sunscreen, cooling towel. The coast is windy and cool even in summer — pack a wind
  layer for the finish and overnight.
- **Wet forecast:** a light rain shell, extra dry socks, and Ziplocs for wet gear.
- **Quad-pounding downhill legs (1–3, 30, 36):** compression and Icy Hot/ice for sore quads
  between legs.
- **Sleeping arrangements:** sleeping bag + pillow are worth it — sleeping fields and vans are
  the norm; even with a safe-house stop (see htc-logistics), bring them.

## Output

Give a clean, checkbox-style list grouped by category (run gear / safety / van / toiletries /
sleep & coast), with the personalized additions flagged so the runner knows why each is there.
Offer to save it as a note in the vault if they want a checklist to tick off.
