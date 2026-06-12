# Identity: Reliance Architecture

> **Slug:** `reliance-architecture`
> **Default for:** Reliance Architecture firm work — client portals, project dashboards, BIM viewers, document exchanges, internal tooling, AEC plugin UIs that surface the firm's brand.
> **Source of truth:** Reliance Architecture Style Guide (created March 2021, Left Hand Design / Beau Morrow). PDF lives at `assets/reliance-architecture/Reliance Architecture Style Guide.pdf`.
> **Concept:** Confident, structural, division-coded. Steel-blue authority on a neutral foundation. The visual language of a firm that builds across Public, Liturgical, Residential, and Commercial work — each division has its own color while the foundation stays consistent.
> **Voice cues:** "Reliable," "specified," "drafted," "engineered," "considered." Avoid "minimal," "quiet," "luxurious" — those belong to Modern Architect.

---

## Identity-Specific Rules (Override Global Defaults)

These exceptions are intentional. Reliance Architecture's brand spec takes precedence over the Modern Architect defaults inside this identity.

1. **White IS allowed.** The firm's brand uses true white surfaces in print and web. On Reliance work, `#FFFFFF` is a valid background — do not substitute Linen.
2. **Neutral Black IS the text token.** `#262626` is the brand-specified dark, not `#2C2F33`.
3. **Montserrat is the type family.** Replace Inter / system fonts. SemiBold for headlines, SemiBold ALL CAPS for subheads, Regular for body.
4. **Division color is contextual.** The active division (Education/Primary, Public, Liturgical, Residential, Commercial) sets the dominant accent. Default to Reliance Steel (Education/Primary) when no division is declared.
5. **Logo gets space.** "Let your logos breathe" is in the brand guide. Reserve at least 1× the logo's height of clear space on all sides in any layout that includes a Reliance mark.

Rules that DO carry over from the universal covenant:
- WCAG 2.1 AA contrast minimums
- 8pt grid for spacing
- ≤ 200ms animation, ease-out
- ≥ 44×44px touch targets
- No tooltips for primary actions
- Skeleton screens (not spinners) for loading
- Localized, actionable error states

---

## Color Palette

### Foundation
| Token | Hex | RGB | Use |
|---|---|---|---|
| Neutral Black | `#262626` | 38, 38, 38 | Primary text. Dark surfaces, footers, reverse-on-white logo backgrounds. **Pantone Neutral Black.** |
| Pure White | `#FFFFFF` | 255, 255, 255 | Primary background. Brand-specified. |
| Slate Mist | `#EDEFF2` | 237, 239, 242 | Secondary panel background (extrapolated from brand neutral). |
| Drafting Gray | `#73777B` | 115, 119, 123 | Secondary text, metadata, captions. |
| Hairline | `rgba(38, 38, 38, 0.12)` | — | Border lines (slightly more present than Modern Architect's 10%). |

### Brand (Primary — Education / Default Division)
| Token | Hex | RGB | Pantone | Use |
|---|---|---|---|---|
| Reliance Steel | `#6B8CA3` | 107, 140, 163 | 5425 | Default primary accent. CTAs, links, active states, brand mark. |
| Deep Steel | `#4F6B7E` | 79, 107, 126 | — | Hover state for Reliance Steel. |
| Light Steel | `#A8B9C6` | 168, 185, 198 | — | Tint variant, soft backgrounds. |

### Division Variants — Swap the primary accent based on project context

The brand uses color-coded divisions. When a project belongs to a division, replace `--accent-primary` (Reliance Steel) with that division's color throughout the UI.

| Division | Token | Hex | RGB | Pantone | Voice cue |
|---|---|---|---|---|---|
| Education / Primary | Reliance Steel | `#6B8CA3` | 107, 140, 163 | 5425 | Authoritative, foundational |
| Public | Public Coral | `#DE614A` | 222, 97, 74 | 7416 | Civic, accessible, warm |
| Liturgical | Liturgical Gold | `#D9AB33` | 217, 171, 51 | 7753 | Sacred, contemplative |
| Residential | Residential Sage | `#6BA391` | 107, 163, 145 | 556 | Domestic, organic, calm |
| Commercial | Commercial Earth | `#B46C42` | 180, 108, 66 | — | Industrious, grounded |

Hover colors for divisions: darken each by ~15% in HSL lightness.

### System Status (universal — same across all Reliance work)
| Token | Hex | Use |
|---|---|---|
| Success | `#4A7A5E` | Confirmed, complete, optimal |
| Warning | `#C9A66B` | Pending, attention needed |
| Error | `#B5392E` | Critical, blocked, destructive |

---

## Typography — Montserrat Stack

Single family across the brand. Hierarchy via weight + scale, same discipline as Modern Architect.

| Role | Family | Weight | Size | Line-height | Letter-spacing |
|---|---|---|---|---|---|
| Display / H1 | Montserrat | 600 (SemiBold) | 32px | 1.2 | 0 |
| H2 | Montserrat | 600 (SemiBold) | 24px | 1.3 | 0 |
| H3 / Subhead | Montserrat | 600 (SemiBold) ALL CAPS | 14px | 1.4 | 0.15em (150 in design tools) |
| Body | Montserrat | 400 (Regular) | 14px | 1.6 | 0 |
| Caption | Montserrat | 400 (Regular) | 12px | 1.5 | 0 |

**Subhead convention** — per the brand guide, subheads are ALL CAPS with wide letter-spacing (tracking 150–600 in Adobe = letter-spacing 0.15em–0.6em in CSS). Use sparingly for section labels and category tags.

**Source:** Montserrat is free on Google Fonts. Include both desktop and webfont versions for production.

**Reading view max width:** 700px (slightly tighter than Modern Architect's 750px — Montserrat reads denser).

---

## Structural Elements

### Borders
- Default hairline: `1px solid rgba(38, 38, 38, 0.12)`
- Slightly more present than Modern Architect — Reliance work tends to have more structural framing (echoing the logo's framed square).

### Elevation / Shadows
```css
/* Resting card */
box-shadow: 0 2px 12px rgba(38, 38, 38, 0.06);

/* Hover lift */
box-shadow: 0 4px 20px rgba(38, 38, 38, 0.10);
```
Tighter, more architectural than Modern Architect's diffuse softness.

### Spacing — 8pt Grid (universal)
Same as Modern Architect: `8, 16, 24, 32, 48, 64, 96, 128`. Sub-component: `4`.

### Border Radius — Tighter
| Element | Radius |
|---|---|
| Small inputs, buttons | `2px` |
| Cards, containers, images | `6px` |
| Pills | Avoid — the brand mark itself is a hard square. |

Sharper corners than Modern Architect (`2/6` vs `4/8`). This mirrors the framed-square logo geometry.

---

## Motion (universal)

| Property | Value |
|---|---|
| Default duration | `150ms` |
| Max duration | `200ms` |
| Easing | `cubic-bezier(0.2, 0.8, 0.2, 1)` |
| Press scale | `transform: scale(0.98)` |
| Hover tint | 8% Neutral Black overlay |

---

## Logo Usage (from Style Guide)

### Three primary marks (all bundled in `assets/reliance-architecture/`)
- **Stacked logo** — icon above wordmark. Use when vertical space allows.
- **Horizontal logo** — icon left of wordmark. Use as the default header mark.
- **Icon only** — framed square `R` mark. Use for app icons, favicons, social avatars, watermarks.

### Files available
- `Reliance Architecture horizontal.svg` — vector, preferred for web
- `Reliance Architecture vertical.svg` — vector, vertical/stacked
- `Reliance Architecture horizontal.png` — raster fallback
- `Reliance Architecture horizontal cropped.pdf` — print-ready cropped horizontal
- `Reliance Architecture Style Guide.pdf` — the authoritative source

### Placement Rules
- Reserve clear space ≥ 1× the icon height on all sides.
- Reverse the logo only on Neutral Black or brand-palette backgrounds, or on images with a color overlay providing sufficient contrast.
- Do NOT recolor the mark outside the palette.
- Do NOT crowd the logo with type or other graphic elements.

### Logo in UI
- App headers: horizontal mark, 32px height, 24px clear space left and right.
- Login / splash screens: stacked mark, centered, 64px height minimum.
- Favicon / browser tab: icon only, exported at 16, 32, 192, 512 px PNG + SVG.

---

## CSS Variables — Drop-In

```css
:root {
  /* Foundation */
  --bg-primary: #FFFFFF;
  --bg-secondary: #EDEFF2;
  --text-primary: #262626;
  --text-secondary: #73777B;
  --border-hairline: rgba(38, 38, 38, 0.12);

  /* Brand — default division (Education / Primary) */
  --accent-primary: #6B8CA3;
  --accent-primary-hover: #4F6B7E;
  --accent-primary-tint: #A8B9C6;

  /* Status */
  --status-ok: #4A7A5E;
  --status-warn: #C9A66B;
  --status-error: #B5392E;

  /* Elevation */
  --shadow-rest: 0 2px 12px rgba(38, 38, 38, 0.06);
  --shadow-hover: 0 4px 20px rgba(38, 38, 38, 0.10);

  /* Geometry */
  --radius-sm: 2px;
  --radius-md: 6px;

  /* Motion */
  --motion-fast: 150ms;
  --motion-default: 200ms;
  --motion-ease: cubic-bezier(0.2, 0.8, 0.2, 1);

  /* Typography */
  --font-family: 'Montserrat', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-weight-body: 400;
  --font-weight-semibold: 600;
}

/* Division variant overrides — apply at the project / route level */
[data-division="public"]      { --accent-primary: #DE614A; --accent-primary-hover: #B84A36; }
[data-division="liturgical"]  { --accent-primary: #D9AB33; --accent-primary-hover: #B08823; }
[data-division="residential"] { --accent-primary: #6BA391; --accent-primary-hover: #4F8475; }
[data-division="commercial"]  { --accent-primary: #B46C42; --accent-primary-hover: #8E5232; }
```

Set `data-division="..."` on `<body>` or root container per project. All accent-driven UI (buttons, links, status badges, active nav items) re-themes automatically.

---

## Disabled State
```css
opacity: 0.4;
cursor: not-allowed;
filter: saturate(0);
```

---

## What Belongs Where (Quick Reference for the Agent)

| Surface | Identity to use |
|---|---|
| Reliance Architecture client portal | Reliance Architecture |
| BIM viewer for a Reliance project | Reliance Architecture (with division variant if known) |
| Internal ArchiCAD plugin for the firm | Reliance Architecture |
| Antonio's personal tools (sweeper, recipe sync) | Modern Architect |
| Side product Antonio ships under his own name | Modern Architect |
| Ayra system surfaces (firm-side) | Reliance Architecture |
| Ayra system surfaces (home-side) | Modern Architect |
