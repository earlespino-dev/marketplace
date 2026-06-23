---
name: htc-logistics
description: Plan the operational side of running Hood to Coast / Portland to Coast as a team — van rotation and leg assignments by team size, major van exchanges, driver shifts, the work-backwards-from-start-time schedule, travel and arrival timing, safe-house strategy, where guests can spectate, the local-team volunteer plan, and race-day flow through to the Seaside finish. Use when asked about vans, drivers, the schedule/itinerary, who runs which leg, exchanges, accommodations, safe houses, volunteers, spectating, or general race-day planning. Owns the per-team config (htc-team-config.md); reads or creates it to remember the team's drivers, lodging, and safe houses.
---

# HTC Team & Race Logistics

Plans how a team actually executes the relay. Generic procedure lives here; team-specific facts
live in the per-team config so they persist across conversations.

## Per-team config

```
<vault_path>/htc-team-config.md
```

Read it at the start of any logistics question; create it from
`${CLAUDE_PLUGIN_ROOT}/skills/htc-logistics/assets/team-config-template.md` the first time, and
update it when team facts change (drivers secured, lodging booked, safe house confirmed). This is
the team-level companion to the per-runner config that htc-setup owns.

## Van rotation & leg assignment

- The active van always carries **6 racers** (one running, five in the van) + a driver. Vans
  swap only at **major exchanges 6, 12, 18, 24, 30**.
- **12-person team:** runner N runs legs **N, N+12, N+24**. Van 1 = runners 1–6 (legs 1–6,
  13–18, 25–30); Van 2 = runners 7–12 (legs 7–12, 19–24, 31–36).
- **8- or 10-person team:** the simple formula breaks — runners rotate through all 36 legs in
  order, wrapping by team size. Use the rotation table in the handbook
  (`${CLAUDE_PLUGIN_ROOT}/references/2026-HTC-Handbook.pdf`, p.16) and the major-van-exchange
  procedure (when a team has fewer than 12, runners shift between vans at the major exchanges to
  keep the active van at six). Confirm against the team's actual assignment.

## Vehicles

Plan for the active van to hold 6 runners + 1 driver = 7 people **plus gear** (clothes, water,
sleep stuff). Large SUVs (Suburban / Ford Expedition Max / Jeep Wagoneer L or similar) hold
people + gear far better than minivans; 13-seater vans are hard to secure (limited / lottery).
Two team signs must be displayed in the van's front and back windows (60-min penalty if not).

## Drivers

Don't make one person drive ~36 hours straight. Either secure a **relief driver per van**, or
have the runners build **driving shifts** among themselves (all six split it, or three take
longer blocks). Night-comfortable drivers are gold for the overnight legs. Record the driver
plan per squad in the team config; flag any van whose drivers are still TBD.

## Schedule: work backwards (and forwards) from the start time

Start times are assigned in a Friday **2:00am–2:00pm** window based on the team pace survey
(faster teams earlier). Once you know it:

- **Backwards:** Van 1 must leave well before the start (e.g. ~3 hrs early — a ~2am departure for
  a ~5am start). That means **Thursday is the prep day** (van pickup, decorate, pack, final prep,
  team bonding), so out-of-towners should **arrive Wednesday, or Thursday early-AM at the latest**.
- **Forwards:** ~36 hours of relay → arrive at the coast Saturday late afternoon/evening → check
  into coast lodging → **Sunday is relaxation/celebration** → **Monday checkout (~11am)**, drive
  back to Portland, fly out Monday evening.
- Collect everyone's travel itinerary early so anyone who must leave Sunday can be put in an early
  car back to Portland ahead of the group.

Predict roughly when each van will reach the next major exchange from the team's paces so the
vans hand off smoothly. (The detailed minute-by-minute timing/driving/exchange spreadsheet is a
separate planning artifact built once the start time is known.)

## Safe houses

If teammates or friends have homes near the route, use them as rest stops instead of exchange
fields — real showers, beds, and a stocked fridge (bananas/Gatorade) beat porta-potties and
sleeping fields. Pick houses near a major exchange (e.g. near Exchange 12), and rely on the
squads being staggered so only ~6 people hit a house at once. Record confirmed safe houses (and
which exchange each is near) in the team config.

## Accommodations & hosting

- **Coast lodging is time-sensitive** — book early before it sells out or the price climbs.
- Local teammates can host out-of-towners before/after the race (cheaper than hotels); collect
  itineraries first, then match hosts to guests. Airport pickup or the Portland MAX train +
  a short pickup are both workable.

## Volunteers (local teams)

A team with any member within 100 miles of Portland must provide **3 volunteers or be
disqualified** (see htc-rules). Be online the instant job selection opens (around 8:00am Pacific)
to grab assignments near the coast (fun) or near Portland (convenient) rather than remote ones.
Track who the three volunteers are and their assignment in the team config.

## Guests / spectating

The only easy places to cheer are the **Portland in-city exchanges** (accessible, can park
nearby) and the **Seaside finish** (beach party). Everything between is remote. Have guests
carpool in team vehicles to meet at the coast; collect their plans alongside the team itinerary.

## Race-day flow & finish

Start-area check-in can be done contactless via the HTC app (photo of safety gear). Designated
sleeping fields exist at exchanges 18, 24, 30. The finish in **Seaside** has a beach party with
food and music; see handbook p.78 for Seaside parking and p.81 for prior race results.
