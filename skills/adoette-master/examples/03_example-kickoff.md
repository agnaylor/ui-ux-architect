# Example Output: ui-project-kickoff

> Reference for what a finished kickoff brief looks like. Notice: platform locked early, hierarchy made explicit, every screen has a Peak-End moment, state map is concrete, tech pick is justified.

---

# Thermomix Recipe Sync — UI/UX Kickoff Brief

**Date:** 2026-06-02
**Platform:** Mobile/Web App (mobile-first)
**Primary User:** Antonio (and other home cooks running multi-Thermomix kitchens)
**Core JTBD:** Take a custom recipe (any format, any source) and push it cleanly onto a specific Thermomix device with zero manual JSON editing.

---

## 1. Platform Rationale
Mobile-first because recipe consumption happens at the counter, phone-in-hand. Web view is responsive scale-up of the same shell, not a separate codebase. The thumb-zone rule governs layout — primary action sits in the lower two-thirds always.

## 2. Information Hierarchy

**Hero (the critical 20%):**
- Current sync target (which Thermomix you're pushing to)
- Currently selected recipe (name + photo)
- One primary CTA: `Sync to <device-name>`

**Progressive Disclosure (the 80%):**
- Recipe library — surfaced via bottom tab `Library`
- Edit recipe steps — surfaced via tap on a recipe row → step editor
- Device management — surfaced via overflow menu `Devices`
- Sync history / logs — surfaced via overflow menu `History`
- Settings / units / language — buried in `Settings` (last tab)

## 3. Key Screens

### Screen A — Home (Sync Pane)
- **Purpose:** Confirm what's about to sync and to which device, then commit.
- **Peak-End Moment:** After successful sync, a snackbar reads `Synced. Recipe ready on <device-name>.` Body fades, status dot on the device card pulses Soft Emerald once, then settles.
- **Primary action:** `Sync to <device-name>` (Blue Agave, lower-third placement).

### Screen B — Recipe Library
- **Purpose:** Browse, search, select a recipe to sync.
- **Peak-End Moment:** Tap-to-select a recipe pulls it up into the hero of Screen A with a subtle 200ms slide-up. No "selected!" toast — the recipe just appears where it belongs.
- **Primary action:** None (browsing is the action).

### Screen C — Recipe Editor
- **Purpose:** Adjust step times, ingredient quantities, temperature targets.
- **Peak-End Moment:** Auto-save on every change. Snackbar `Draft saved.` only on first edit per session — not on every change (that'd be noise).
- **Primary action:** `Save and return` (Blue Agave, bottom-right).

### Screen D — Devices
- **Purpose:** Pair a new Thermomix, rename, remove.
- **Peak-End Moment:** Successful pairing → device card animates in from the bottom with a soft elevation. Body text: `Connected to <device-name>.`
- **Primary action:** `Add a Thermomix` (Blue Agave, full-width in lower third).

### Screen E — History
- **Purpose:** Audit log. What synced when, to which device, success/fail.
- **Peak-End Moment:** None — this is a backward-looking utility, not a forward-looking workflow.
- **Primary action:** None. Each row taps into a detail view.

## 4. Component Inventory

**Reuse from system:**
- Button (primary Blue Agave, ghost, destructive)
- Card (resting + hover elevation)
- StatusBadge (ok / warn / error) — see `examples/02_example-component.md`
- Snackbar (bottom-right, 3s auto-dismiss)
- Skeleton (Warm Ash pulse gradient)

**New components needed:**
- `RecipeCard` — photo + title + cook time + Sync button on long-press
- `DeviceCard` — device name + connection status + last-sync timestamp
- `StepEditor` — inline-editable cooking step with time/temp/speed controls
- `IngredientList` — auto-formatted ingredient lines with quantity adjusters
- `SyncProgressBar` — determinate bar for the actual sync push (Bluetooth latency)

## 5. State Map

| Screen | Default | Loading | Empty | Error |
|---|---|---|---|---|
| Home | Recipe card + Sync CTA | Skeleton recipe card + disabled Sync | `Pick a recipe to sync` → opens Library | `Can't reach <device>. Reconnect.` inline below CTA |
| Library | Recipe grid | Skeleton grid (8 placeholder cards) | `No recipes yet` → `Import a recipe` | `Couldn't load library. Retry.` full-pane |
| Editor | Form with current values | Skeleton form | N/A (always opens with data) | Inline per-field validation |
| Devices | Device list | Skeleton device cards | `No Thermomix paired` → `Add a Thermomix` | Per-card status: `Disconnected. Reconnect.` |
| History | Log table | Skeleton rows | `No sync history yet.` (no CTA — natural state for new users) | Row-level: red icon + tap for details |

## 6. Tech Stack

- **Front-end:** TypeScript + React Native (Expo Go for dev, EAS Build for ship)
- **Back-end:** Python (FastAPI) for recipe parsing, format conversion, sync orchestration
- **Bluetooth/device layer:** Native module bridge (Swift on iOS, Kotlin on Android) — Thermomix BLE protocol isn't fully covered by RN libraries
- **Why:** TS gives instant UI state response (mobile blueprint demands it). Python handles the messy recipe-format normalization (markdown → JSON → Thermomix proprietary format). Native module is unavoidable for BLE on iOS.
- **Risks:**
  - **Thermomix BLE handshake** is undocumented — budget 2 weeks of reverse engineering before committing to ship date.
  - **Recipe format zoo** — every source site has different structure. Build the parser layer with explicit per-source adapters, don't try to write a universal parser.

## 7. Build Order

**Sprint 1 — Foundation (2 weeks):**
- Design system in code: tokens, Button, Card, Snackbar, Skeleton
- Home screen shell + Devices screen
- Mock sync (no real BLE yet) to validate the flow

**Sprint 2 — Real Sync (2 weeks):**
- Native BLE module + device pairing
- Library + recipe selection
- Real sync push with progress bar

**Sprint 3 — Editing + Polish (2 weeks):**
- Recipe editor + auto-save
- History screen
- Accessibility audit + state map verification
- Pre-ship: WCAG AA scan, all four states tested per screen

## 8. Audit Plan

- After Sprint 1: run `ui-accessibility-audit` against Home + Devices shells.
- After Sprint 2: run `ui-design-critique` against the sync flow end-to-end.
- Pre-ship: full audit pass + Antonio reviews with real recipes on a real Thermomix in his kitchen.

---

## Open Questions for Antonio

1. **Recipe sources:** Is the v1 scope "paste markdown/JSON" or do we need scrapers for AllRecipes, Bon Appétit, etc.?
2. **Multi-device sync:** Sync one recipe to multiple Thermomixes at once, or strictly 1:1?
3. **Offline mode:** Must the app work without internet (recipe edit + queue sync) or is online assumed?
