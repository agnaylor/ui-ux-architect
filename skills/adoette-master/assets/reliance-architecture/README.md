# Reliance Architecture — Brand Assets

## Bundled in this plugin

| File | Use |
|---|---|
| `RA-Icon-Color.svg` | Primary icon, brand steel `#6B8CA3`. Default for favicons, app icons, watermarks. |
| `RA-Icon-Black.svg` | Single-color icon for light backgrounds. |
| `RA-Icon-White.svg` | Single-color icon for dark backgrounds. |
| `RA-Icon-Public.svg` | Public Architecture division — `#DE614A`. |
| `RA-Icon-Liturgical.svg` | Liturgical Architecture division — `#D9AB33`. |
| `RA-Icon-Residential.svg` | Residential Architecture division — `#6BA391`. |
| `RA-Icon-Commercial.svg` | Commercial Architecture division — `#B46C42`. |
| `Reliance Architecture Style Guide.pdf` | Authoritative brand source (Left Hand Design, March 2021). |

## Full asset library (firm's Dropbox)

The complete logo asset library — horizontal wordmark, stacked wordmark, EPS, PDF, PNG variants in every color treatment — lives at:

```
Z:\RA Dropbox\Marketing\Logo & Style Guide\2021 Logo\
```

Subfolders:
- `1-Primary/` — primary brand (Education / default Steel)
- `2-Public Architecture/` — Public Coral variants
- `3-Commercial Architecture/` — Commercial Earth variants
- `4-Sustainable Architecture/` — sustainability variant set
- `5-Residential Architecture/` — Residential Sage variants

Each contains `Vector/` (EPS, PDF, SVG) and `Web/` (JPG, PNG) subdirectories with Black, Color, Reversed, and White treatments.

**For production deliverables**, pull from the Dropbox folder above — the icons bundled here are for in-app UI use (favicons, headers, watermarks at small-to-medium sizes).

## Logo embedding patterns

### Inline SVG (recommended for UI)
```tsx
import RAIcon from '@/assets/reliance-architecture/RA-Icon-Color.svg';

<RAIcon className="logo-mark" aria-label="Reliance Architecture" />
```

### Division-aware logo component
```tsx
import { divisionLogo } from '@/assets/reliance-architecture';

<img
  src={divisionLogo(currentProject.division)}
  alt={`Reliance Architecture — ${currentProject.division}`}
  height={32}
/>
```

## Clear-space rules

Reserve at least **1× the icon height** of clear space on all sides. In a 32px header logo, leave 24–32px of breathing room.

The brand mark is the framed square. Do not crop it, recolor it outside the palette, or stretch it.
