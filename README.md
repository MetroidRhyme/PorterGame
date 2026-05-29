# PORTER

A location-based walking game played in your real neighborhood. Walk the streets, pick up packages, and deliver them across your zone to score points.

**Play it:** open `index.html` in a mobile browser. No server or install required.

---

## How to play

1. **Grant GPS access** when prompted. The map will center on your location once locked.
2. **Draw a zone** — tap ☰ → **+ ADD ZONE**, then tap hex cells on the map to define your play area. Tap **FINISH ZONE** when done.
3. **Pick up packages** (📦) by walking within 20 m of them.
4. **Deliver** them to drop zones (🏠) to score points.

Packages are scored by `distance × weight multiplier`. Each package carries a randomly assigned item name (Birthday Cake, Vintage Records, Medical Supplies, etc.) shown in the HUD and on the map.

Your carry capacity starts at 3 units and grows by 1 for every 500 points, up to a max of 12. A **CAP X · Y TO ↑** indicator appears under the score so you always know how close the next upgrade is.

**Delivery streaks** — consecutive deliveries without abandoning a package build a streak counter shown in the completion flash. Abandoning any package resets the streak to zero.

### Package weights

| Weight | Units | Multiplier |
|--------|-------|------------|
| Light    | 1 u | 0.7× |
| Standard | 2 u | 1.0× |
| Heavy    | 3 u | 1.5× |

---

## Zones

Zones are made of hex grid cells (~20 m circumradius, ~400 m² each). You can define multiple named zones in different colors; packages and destinations only spawn in active zones.

You can paint your entire accessible area, or place just a handful of hexes in specific spots — orders only spawn on painted cells, giving you full control over where the action is. For zones with fewer total hexes the order count scales more generously per hex to keep play density reasonable.

- **Draw mode** — tap cells to add/remove them. Disconnected selections become separate zones automatically. After saving your first zone a tip toast will point you to Paint mode.
- **Paint mode** — enable follow + select a zone from the picker, then walk to paint cells as you move.
- **Edit** an existing zone from Settings to resize or reshape it.
- **Adjust zone position** — use the arrow pad to shift the hex grid alignment if cells don't line up with streets.

---

## UI controls

| Control | Action |
|---------|--------|
| ☰ (top left) | Open Settings |
| ↻ (top) | Refresh orders (clears all packages) |
| ◎ (top right) | Toggle follow mode / open paint picker |
| Pull handle (bottom) | Collapse/expand the HUD panel |
| Action button | Context-sensitive: pick up, deliver, draw, or open settings |

---

## Settings

- **Zones** — add, edit, toggle, share, or delete zones
- **Profile** — set your display name; share your score
- **Data** — export save file (`.json`), import save file or shared zone (`.porter`), reset all data

### Sharing

- **Share Zone** (↑ next to a zone) — exports a `.porter` file containing that zone's hex cells. Import it on another device to copy the zone layout.
- **Share Profile** — shares your name and score via the native share sheet or copies to clipboard.

---

## Technical notes

- **Single file** — the entire game is `index.html` with no build step.
- **Dependencies** — [Leaflet 1.9.4](https://leafletjs.com/) loaded from CDN; [CartoDB light](https://carto.com/basemaps/) map tiles.
- **Storage** — all state is in `localStorage` under `porter_*` keys. No backend.
- **Hex grid** — flat-top axial coordinates (q, r). Cell size is ~20 m (~0.00018°) latitude; longitude is corrected for the player's latitude on first GPS lock.
- **Proximity** — pickup and delivery both require being within 20 m (`PROXIMITY_M`).
- **Auto-refresh** — if a zone is too small to fit new packages and destinations, the game schedules a 30-second retry rather than silently failing.
