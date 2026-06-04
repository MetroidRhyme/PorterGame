# PORTER

A location-based walking game played in your real neighborhood. Walk the streets, pick up packages, and deliver them across your zone to score points.

**Play it:** open `index.html` in a mobile browser. No server or install required.

---

## How to play

1. **Grant GPS access** when prompted. The map will center on your location once locked.
2. **Draw a zone** — tap ⋮ → **SETTINGS** → **+ ADD ZONE**, then tap hex cells on the map to define your play area. Tap **FINISH ZONE** when done.
3. **Pick up packages** (📦) by walking within 30 m of them.
4. **Deliver** them to **drops** — lettered points on the map — to score points.

Packages are scored by `distance × weight multiplier`. Each package carries a randomly assigned item name (Birthday Cake, Vintage Records, Medical Supplies, etc.) shown in the HUD and on the map.

### On-screen cues

The game surfaces what you can do right now:

- The nearest **pickable package** gently bobs once you're in range and have spare capacity for it.
- The **action button** pulses — amber for pickup, blue for delivery — when an action is ready.
- The **drop you're delivering to** lights up with a glow when you're carrying for it and within range.
- Your **position marker** glides smoothly between GPS updates instead of jumping.

### Package weights

| Weight | Units | Multiplier |
|--------|-------|------------|
| Light    | 1 u | 0.7× |
| Standard | 2 u | 1.0× |
| Heavy    | 3 u | 1.5× |

---

## Levels & upgrades

Your **player level** is derived from your total score on a rising curve (level 1 ≈ 150 pts; level 50 ≈ 31k pts), capping at level 50. The score display shows your current level and the points remaining to the next one — tap it to open the full upgrade track.

Carry capacity starts at 3 units and grows by 1 at levels 10, 20, 30, 40, and 50 (max **8 units**). Higher levels also unlock and upgrade your drone.

| Level | Unlock |
|-------|--------|
| 10 | Carry capacity +1 (4 u) |
| 15 | **Drone** unlocked — light packages, 10-hex range, 3 h cooldown |
| 20 | Carry capacity +1 (5 u) |
| 25 | Drone upgrade — standard & lighter, 20-hex range, 2 h cooldown |
| 30 | Carry capacity +1 (6 u) |
| 35 | Drone upgrade — all weights, 30-hex range, 1 h cooldown |
| 40 | Carry capacity +1 (7 u) |
| 45 | Second drone slot (both share a 1 h cooldown) |
| 50 | Carry capacity +1 (8 u) · max level |

---

## Drones

Once unlocked at level 15, a drone can deliver a package for you without walking it to the drop — useful for far or awkward destinations. You can launch one from a nearby package (**Drone Lift**) or from something you're already carrying (the **Drone** button in your inventory).

- Drone deliveries are worth **half** the package's points (the level bonus below does **not** apply).
- The destination drop must be within the drone's hex **range**, and the package must be within the drone's **weight tier**.
- Each use puts the drone on **cooldown**; level 45 adds a second drone so you can have two in flight.

| Player level | Carries | Range | Cooldown |
|--------------|---------|-------|----------|
| 15 | Light | 10 hex | 3 h |
| 25 | Standard & lighter | 20 hex | 2 h |
| 35 | All weights | 30 hex | 1 h |
| 45 | (adds a second drone, shared 1 h cooldown) | | |

Drones in flight are saved, so they keep traveling — and complete — even if you close the game.

---

## Drops

Drops are the lettered delivery points that orders are routed to. Each is auto-named (e.g. "Alice Chen") and **levels up** as points are delivered to it, on the same curve as player level.

- A drop's level grants a **delivery bonus**: walked deliveries to it earn an extra **+1% per drop level**.
- After a delivery, a drop waits ~5 minutes, then spawns fresh packages around itself.
- Drops are **permanent**: they keep their level, points, and contributors even after their zone is deleted (they simply go **dormant** until a zone covers them again).

Tap a drop to open its panel, see its level and progress, and use level-gated upgrades:

| Drop level | Upgrade |
|------------|---------|
| 5  | Rename the drop |
| 10 | Change its icon |
| 20 | Relocate it (must stay inside a zone, ≥5 hexes from other drops, 24 h cooldown) |

---

## Zones

Zones are made of hex grid cells (~20 m circumradius, ~1,040 m² each). You can define multiple named zones in different colors; packages and drops only spawn in **active** zones. For zones with fewer total hexes the order count scales more generously per hex to keep play density reasonable.

You can paint your entire accessible area, or place just a handful of hexes in specific spots — orders only spawn on painted cells, giving you full control over where the action is.

- **Draw mode** — tap cells to add/remove them. After saving your first zone a tip toast points you to Paint mode.
- **Paint mode** — pick a zone from the picker, then walk to paint cells onto it as you move.
- **Edit** an existing zone from Settings to resize or reshape it.
- **Merge** one zone into another (its cells and any drops move into the target).
- **Toggle** a zone active/inactive without deleting it.
- **Adjust zone position** — use the arrow pad to shift the hex grid alignment if cells don't line up with streets.

---

## UI controls

| Control | Action |
|---------|--------|
| ⋮ (top right) | Open the menu (Follow · Paint · Refresh · Settings) |
| Level / score (top left) | Tap to view your upgrade track |
| Pull handle (bottom) | Collapse/expand the HUD panel |
| Action button | Context-sensitive: pick up, deliver, finish a zone, or open settings |

The **menu** holds:

- **Follow** — keep the map centered on you as you walk.
- **Paint** — choose a zone, then paint cells onto it as you move.
- **Refresh** — clear current packages (including carried ones) and generate new ones. You must be standing at a drop, and it has a 1-minute cooldown. Your drops are kept.
- **Settings** — open the settings drawer.

---

## Settings

- **Zones** — add, edit, toggle, merge, or delete zones; adjust grid alignment.
- **Profile** — set your display name (shown on drops you've contributed to).
- **Data** — export a full save backup (`.json`), import a backup, or reset all data.

---

## Technical notes

- **Single file** — the entire game is `index.html` with no build step.
- **Dependencies** — [Leaflet 1.9.4](https://leafletjs.com/) loaded from CDN; [CartoDB light](https://carto.com/basemaps/) map tiles.
- **Storage** — all state is in `localStorage` under `porter_*` keys. No backend. Corrupted keys fall back to defaults rather than breaking load.
- **Reduced motion** — all animated cues, panel/modal transitions, and the marker glide honor the OS `prefers-reduced-motion` setting and fall back to a static UI.
- **Hex grid** — flat-top axial coordinates (q, r). Cell size is ~20 m (~0.00018°) latitude; longitude is corrected for the player's latitude on first GPS lock.
- **Proximity** — pickup and delivery both require being within 30 m (`PROXIMITY_M`).
- **Spawning** — packages spawn in distance bands around each drop, with a minimum of one drop per active zone. After a delivery a drop re-spawns packages on a ~5-minute delay.
- **Auto-refresh** — if a zone is too small to fit new packages and drops, the game schedules a 30-second retry rather than silently failing.
- **Drop persistence** — drops are permanent: they keep their level, points, and contributors even after their zone is deleted (they go dormant). To keep saves bounded, never-used auto-generated drops (no deliveries, points, or contributors) whose zone is gone are pruned on load.
- **Share/sync codes** — code exists for sharing zones, drops, and bulk drop stats via text codes, but those Settings sections are currently disabled in the UI; only save-file export/import is exposed.
