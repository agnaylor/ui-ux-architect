# Identity: [Brand Name]

> Copy this file, rename it to `<slug>.md` (kebab-case), and fill in every section. Delete any section that genuinely does not apply, but most should be filled. When the identity is complete, register it in `_index.md` so Adoette can route to it.

> **Slug:** `your-slug-here`
> **Default for:** [Describe which projects should use this identity by default.]
> **Source of truth:** [Style guide PDF? Brand book? Founder's preference? Cite the authority.]
> **Concept:** [One paragraph. What's the visual personality? What does it remind you of? What does it explicitly NOT remind you of?]
> **Voice cues:** [Five to seven adjectives this brand uses to describe itself. Five to seven adjectives it actively avoids.]

---

## Identity-Specific Rules (Override Global Defaults)

List every rule where this identity intentionally departs from the universal covenant. Be explicit — the agent will enforce the override.

1. [e.g., "Pure white IS allowed."]
2. [e.g., "Type family is X, not Y."]
3. [e.g., "Use brand red for primary CTAs, not a neutral accent."]

Rules that DO carry over from the universal covenant (these never bend, regardless of identity):
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
| [Bg Primary] | `#______` | __, __, __ | Primary background. |
| [Bg Secondary] | `#______` | __, __, __ | Secondary panel background. |
| [Text Primary] | `#______` | __, __, __ | Primary text. |
| [Text Secondary] | `#______` | __, __, __ | Secondary text, metadata, captions. |
| Hairline | `rgba(__, __, __, 0.__)` | — | Default border line. |

### Brand
| Token | Hex | Pantone (if any) | Use |
|---|---|---|---|
| [Primary] | `#______` | — | Default primary accent. CTAs, links, active states. |
| [Primary Hover] | `#______` | — | Hover state. |
| [Secondary Accent] | `#______` | — | Secondary accent, badges, highlights. |

### Variant Set (if the brand uses divisional or contextual color coding)
| Variant | Token | Hex | Use |
|---|---|---|---|
| [e.g., Division A] | | | |
| [e.g., Division B] | | | |

### System Status (universal — keep consistent across identities for legibility)
| Token | Hex | Use |
|---|---|---|
| Success | `#______` | Confirmed, complete, optimal. |
| Warning | `#______` | Pending, attention needed. |
| Error | `#______` | Critical, blocked, destructive. |

---

## Typography

| Role | Family | Weight | Size | Line-height | Letter-spacing |
|---|---|---|---|---|---|
| Display / H1 | | | 32px | 1.2 | |
| H2 | | | 24px | 1.3 | |
| H3 / Subhead | | | 18px | 1.4 | |
| Body | | | 14px | 1.6 | |
| Caption | | | 12px | 1.5 | |

**Source / licensing:** [Where to obtain the font. Google Fonts? MyFonts purchase required? Custom foundry?]

**Reading view max width:** ____ px

---

## Structural Elements

### Borders
- Default hairline: `1px solid rgba(__, __, __, 0.__)`
- Notes: [Does this brand prefer visible structure or whitespace separation?]

### Elevation / Shadows
```css
/* Resting */
box-shadow: 0 __px __px rgba(__, __, __, 0.__);

/* Hover */
box-shadow: 0 __px __px rgba(__, __, __, 0.__);
```

### Spacing — 8pt Grid (universal)
`8, 16, 24, 32, 48, 64, 96, 128`. Sub-component fine-tuning: `4` permitted.

### Border Radius
| Element | Radius |
|---|---|
| Small inputs, buttons | `___px` |
| Cards, containers, images | `___px` |
| Pills | [Allowed or avoided? Why?] |

---

## Motion (universal)

| Property | Value |
|---|---|
| Default duration | `150ms` |
| Max duration | `200ms` |
| Easing | `cubic-bezier(0.2, 0.8, 0.2, 1)` |
| Press scale | `transform: scale(0.98)` |

---

## Logo Usage (if a logo exists for this brand)

### Files bundled
List the SVG / PNG / PDF files in `assets/<slug>/`.

### Clear-space rules
[e.g., "1× icon height all sides."]

### Placement rules
- App headers: [size + clear space]
- Login / splash: [size + placement]
- Favicon / browser tab: [export sizes]

### Forbidden
- [Recolor outside palette? Cropping? Stretching?]

---

## CSS Variables — Drop-In

```css
:root {
  /* Foundation */
  --bg-primary: #______;
  --bg-secondary: #______;
  --text-primary: #______;
  --text-secondary: #______;
  --border-hairline: rgba(__, __, __, 0.__);

  /* Brand */
  --accent-primary: #______;
  --accent-primary-hover: #______;
  --accent-secondary: #______;

  /* Status */
  --status-ok: #______;
  --status-warn: #______;
  --status-error: #______;

  /* Elevation */
  --shadow-rest: 0 __px __px rgba(__, __, __, 0.__);
  --shadow-hover: 0 __px __px rgba(__, __, __, 0.__);

  /* Geometry */
  --radius-sm: __px;
  --radius-md: __px;

  /* Motion */
  --motion-fast: 150ms;
  --motion-default: 200ms;
  --motion-ease: cubic-bezier(0.2, 0.8, 0.2, 1);

  /* Typography */
  --font-family: '______', -apple-system, sans-serif;
  --font-weight-body: 400;
  --font-weight-semibold: 600;
}
```

### Variant overrides (if applicable)
```css
[data-variant="______"] { --accent-primary: #______; --accent-primary-hover: #______; }
```

---

## Disabled State (universal)
```css
opacity: 0.4;
cursor: not-allowed;
filter: saturate(0);
```

---

## What Belongs Where (Routing Hints for Adoette)

| Surface | Use this identity? |
|---|---|
| [Description of project A] | Yes |
| [Description of project B] | Yes |
| [Description of out-of-scope work] | No — route to [other identity] |

---

## Registration Checklist

Before this identity is ready for use:

- [ ] Filename is `<slug>.md`, slug is kebab-case
- [ ] All token tables filled
- [ ] CSS variables block compiles
- [ ] Logo assets (if any) bundled in `assets/<slug>/`
- [ ] Style-guide source PDF (if any) bundled in `assets/<slug>/`
- [ ] Entry added to `_index.md`
- [ ] Adoette SKILL.md routing table includes this identity
- [ ] Tested: open `assets/<slug>/showcase.html` (if built) for visual sanity check
