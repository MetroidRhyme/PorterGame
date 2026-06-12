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
- **Drops** appear as flat-top hex icons that fill their map cell; the one you're delivering to gains a blue glow when you're in range.
- **Depots** appear as hex icons too; a green border shows when you're close enough to use one.
- Your **position marker** glides smoothly between GPS updates instead of jumping.

### Package weights

| Weight | Units | Multiplier |
|--------|-------|------------|
| Light    | 1 u | 0.7× |
| Standard | 2 u | 1.0× |
| Heavy    | 3 u | 1.5× |

---

## Levels & the skill tree

Your **player level** is derived from your total score on a rising curve (level 1 ≈ 150 pts; level 50 ≈ 31k pts), capping at level 50. **Every level earns one skill point.** Tap the level display (top left) to open the **skill tree** — drawn as a connected node graph growing down from a root LV node into three branches. Tap any node to inspect it and unlock it from the detail card; an amber `SP` badge under your level shows when you have unspent points.

All node costs sum to exactly **50 points**, so a max-level player can eventually own the whole tree — the build order is the choice. There are no minimum-level gates: cost and the connections shown in the tree are the only limits, so saving early points to rush a drone is a legitimate strategy.

| Branch | Paths (cost) |
|--------|--------------|
| **PORTER** | Carry +1 (2) → Carry chain to 8 u (2/3/3/4) · Carry +1 → Grapple Hook (2) → Long Throw (1) → Fast Reel (1) |
| **AIRFRAME** | Light Drone (3) → Extended Rotors (1) → Careful Courier (1) / Quick Charge (2) · Light Drone → Medium Drone (4) → Heavy Drone (5) |
| **NETWORK** | Depot I (2) → Tall Shelves (1) · Depot I → Depot II (2) → Depots III–V (2/1/1) · Depot II → Porter-Bot I (2) → Cargo Rack (1) / Bot II (2) → Bot III (2) |

**Respec** — a button at the bottom of the tree refunds all spent points, on a 24-hour cooldown. Depots already placed keep working (you just can't place new ones beyond your allocation), and bots beyond your allocation are retired as soon as they aren't carrying anything.

Saves from v1 are migrated automatically: you get points equal to your level and re-pick your build.

---

## Grapple hook

A 2-point PORTER skill, branching off the first Carry node. When charged, a 🪝 button sits beside the action button, and a dotted purple line and reticle mark the closest package within **2 hexes** (3 with Long Throw). Tap to fire the hook and reel the package straight into your inventory — any weight works, as long as you have free carry space. After use the button greys out and visibly refills over its **15-minute cooldown** (10 with Fast Reel).

---

## Drones

Three independent drones are bought as AIRFRAME skills (Light → Medium → Heavy), each with its own cooldown ring shown on the capacity bar. A drone delivers a package for you without walking it to the drop — useful for far or awkward destinations. You can launch one from a nearby package (**Drone Lift**) or from something you're already carrying (the **Drone** button in your inventory); the game automatically uses the lightest ready drone that can carry and reach the package.

- Drone deliveries are worth **half** the package's points — 60% with the Careful Courier skill (the drop level bonus does **not** apply).
- The destination drop must be within the drone's hex **range** (+25% with Extended Rotors), and the package must be within the drone's **weight tier**.
- Each drone recharges independently (cooldowns −25% with Quick Charge), so heavier drones stay available while a lighter one cools down.

| Drone | Cost | Carries | Base range | Base cooldown |
|-------|------|---------|------------|---------------|
| Light  | 3 SP | Light only | 10 hex | 1 h |
| Medium | 4 SP | Standard & lighter | 20 hex | 2 h |
| Heavy  | 5 SP | All weights | 30 hex | 3 h |

Drones in flight are saved, so they keep traveling — and complete — even if you close the game.

---

## Depots

Storage depots are physical stash points you place on the map. Up to five are bought as NETWORK skills, and the Tall Shelves skill raises each depot's storage from 10 to 15 weight units.

To place one, tap **⋮ → PLACE DEPOT** and confirm at your current location. Walk within range and tap its hex icon to open the **transfer menu** — move packages between your inventory and the depot's storage.

Depots appear on the map as hex icons, matching the same style as drops. A **green border** indicates you're within range.

### Porter-bots

Up to three porter-bots are bought as NETWORK skills (Porter-Bot I needs Depot II — bots only matter once packages can move *between* depots). An idle bot automatically shuttles packages from any depot to whichever other depot is closer to each package's destination — no input needed. Each bot carries up to **3 weight units** at a time (5 with Cargo Rack).

Idle bots rest inside a depot; tap any depot to see how many are stationed there.

---

## Drops

Drops are the lettered delivery points that orders are routed to. Each is auto-named (e.g. "Alice Chen") and **levels up** as points are delivered to it, on the same curve as player level.

- A drop's level grants a **delivery bonus**: walked deliveries to it earn an extra **+1% per drop level**.
- After a delivery, a drop waits ~15 minutes, then spawns fresh packages around itself.
- Drops are **permanent**: they keep their level, points, and contributors even after their zone is deleted (they simply go **dormant** until a zone covers them again).

Tap a drop to open its panel, see its level and progress, and use level-gated upgrades:

| Drop level | Upgrade |
|------------|---------|
| 5  | Rename the drop |
| 10 | Change its icon |
| 20 | Relocate it (must stay inside a zone, ≥5 hexes from other drops, 24 h cooldown) |

---

## Collection

Every package carries one of **24 item types** (Birthday Cake, Vintage Records, Fragile Glassware…). Delivering them fills a Pokédex-style **collection**: tap **⋮ → SETTINGS → COLLECTION → VIEW DELIVERY LOG** to see how many types you've discovered, your total deliveries logged, and a per-item delivered count. Undiscovered types show as `???` until you deliver one.

The first time you deliver a new item type — on foot or by drone — the game flags the discovery, so there's always one more box to fill. Collection progress is tracked per item across walked and drone deliveries alike, and is included in save-file export/import.

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
| Level / score (top left) | Tap to open the skill tree |
| Pull handle (bottom) | Collapse/expand the HUD panel |
| Action button | Context-sensitive: pick up, deliver, finish a zone, or open settings |

The **menu** holds:

- **Follow** — keep the map centered on you as you walk.
- **Paint** — choose a zone, then paint cells onto it as you move.
- **Refresh** — clear current packages (including carried ones) and generate new ones. You must be standing at a drop, and it has a 1-minute cooldown. Your drops, depot-stored packages, and packages in bot transit are kept.
- **Settings** — open the settings drawer.

---

## Settings

- **Zones** — add, edit, toggle, merge, or delete zones; adjust grid alignment.
- **Profile** — set your display name (shown on drops you've contributed to).
- **Collection** — open your delivery log: every item type, with discovered count and per-item totals.
- **Data** — export a full save backup (`.json`), import a backup, or reset all data.

---

## Technical notes

- **Single file** — the entire game is `index.html` with no build step.
- **Dependencies** — [Leaflet 1.9.4](https://leafletjs.com/) loaded from CDN; [CartoDB light](https://carto.com/basemaps/) map tiles.
- **Storage** — all state is in `localStorage` under `porter_*` keys. No backend. Corrupted keys fall back to defaults rather than breaking load.
- **Reduced motion** — all animated cues, panel/modal transitions, and the marker glide honor the OS `prefers-reduced-motion` setting and fall back to a static UI.
- **Hex grid** — flat-top axial coordinates (q, r). Cell size is ~20 m (~0.00018°) latitude; longitude is corrected for the player's latitude on first GPS lock.
- **Proximity** — pickup and delivery both require being within 30 m (`PROXIMITY_M`).
- **Spawning** — packages spawn in distance bands around each drop, with a minimum of one drop per active zone. After a delivery a drop re-spawns packages on a ~15-minute delay.
- **Auto-refresh** — if a zone is too small to fit new packages and drops, the game schedules a 30-second retry rather than silently failing.
- **Drop persistence** — drops are permanent: they keep their level, points, and contributors even after their zone is deleted (they go dormant). To keep saves bounded, never-used auto-generated drops (no deliveries, points, or contributors) whose zone is gone are pruned on load.
- **Share/sync codes** — code exists for sharing zones, drops, and bulk drop stats via text codes, but those Settings sections are currently disabled in the UI; only save-file export/import is exposed.
