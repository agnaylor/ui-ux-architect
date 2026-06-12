# Identity: Modern Architect

> **Slug:** `modern-architect`
> **Default for:** Personal projects, side work, products Antonio ships under his own name.
> **Concept:** Quiet Luxury. Modern architectural principles — clean lines, honest materials, open space. Earth tones, soft elevation, generous whitespace.
> **Voice cues:** "Quiet," "honest," "considered," "timeless," "frictionless."

> Source of truth for every CSS variable, Tailwind config, or inline style generated under this identity. Do not invent new tokens — extend this file first.

## Color Palette

### Foundation (Earth Tones & Neutrals)
| Token | Hex | Use |
|---|---|---|
| Linen | `#F7F6F2` | Primary background — replaces `#FFFFFF` |
| Warm Ash | `#EAE9E5` | Secondary background, panels, skeleton-screen base |
| Chimney Smoke | `#2C2F33` | Primary text — replaces `#000000` |
| Herringbone Gray | `#73777B` | Secondary text, metadata, captions |

### Brand & Interaction
| Token | Hex | Use |
|---|---|---|
| Blue Agave | `#5A727A` | Primary accent — CTAs, active states |
| Deep Agave | `#43575E` | Hover state for primary CTAs |
| Muted Terracotta | `#B4846C` | Secondary accent, badges, selective highlights |

### System Status (Desaturated)
| Token | Suggested Hex | Use |
|---|---|---|
| Soft Emerald | `#6B9A85` | Optimal / success / active |
| Soft Amber | `#C9A66B` | Warning / pending / reconnecting |
| High-Contrast Crimson | `#B5482F` | Critical / error / destructive |

## Borders
- Default: `1px solid rgba(44, 47, 51, 0.1)` (Chimney Smoke @ 10%)
- Prefer **negative space** over visible borders wherever Law of Proximity permits it.

## Elevation / Shadows
```css
/* Resting card */
box-shadow: 0 4px 24px rgba(44, 47, 51, 0.04);

/* Hover lift */
box-shadow: 0 8px 32px rgba(44, 47, 51, 0.08);
```
Avoid hard, dark, or directional drop shadows. Light comes from above, diffuse.

## Spacing — 8pt Grid
Allowed values (px): `8, 16, 24, 32, 48, 64, 96, 128`
Sub-component fine-tuning (icons, label offsets): `4` permitted.
**Forbidden:** `5, 7, 10, 13, 15, 18, 20` and similar off-grid values.

## Border Radius
| Element | Radius |
|---|---|
| Small inputs, buttons | `4px` |
| Cards, containers, images | `8px` |
| Pills | Avoid unless the surface is intentionally casual |

## Typography Scale
Single sans-serif family (Inter, SF Pro, or system). Hierarchy via weight + scale, not family swaps.

| Role | Size | Weight | Line-height |
|---|---|---|---|
| Body | 14px | 400 | 1.6 |
| H3 | 18px | 500 | 1.4 |
| H2 | 24px | 600 | 1.3 |
| H1 | 32px | 700 | 1.2 |
| Caption | 12px | 400 | 1.5 |

Reading-view max width: **650–750px**.

## Motion
| Property | Value |
|---|---|
| Default duration | `150ms` |
| Max duration | `200ms` |
| Easing | `cubic-bezier(0.2, 0.8, 0.2, 1)` (ease-out) |
| Press scale | `transform: scale(0.98)` |
| Hover tint | 5% overlay or `Warm Ash` background swap |

## Disabled State
```css
opacity: 0.4;
cursor: not-allowed;
filter: saturate(0);
```

## CSS Variables (Drop-In)
```css
:root {
  --bg-primary: #F7F6F2;
  --bg-secondary: #EAE9E5;
  --text-primary: #2C2F33;
  --text-secondary: #73777B;
  --accent-primary: #5A727A;
  --accent-primary-hover: #43575E;
  --accent-secondary: #B4846C;
  --status-ok: #6B9A85;
  --status-warn: #C9A66B;
  --status-error: #B5482F;
  --border-hairline: rgba(44, 47, 51, 0.1);
  --shadow-rest: 0 4px 24px rgba(44, 47, 51, 0.04);
  --shadow-hover: 0 8px 32px rgba(44, 47, 51, 0.08);
  --radius-sm: 4px;
  --radius-md: 8px;
  --motion-fast: 150ms;
  --motion-default: 200ms;
  --motion-ease: cubic-bezier(0.2, 0.8, 0.2, 1);
}
```
