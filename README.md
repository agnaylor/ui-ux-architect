# ui-ux-architect

> Multi-identity UI/UX design system for Antonio Naylor.
> A portable Claude Code + Cowork plugin. Two production identities, a template for more, five named agents handling the full UI/UX workflow.

## What This Plugin Does

Loads Antonio's complete UI/UX covenant — design tokens, platform blueprints, component specs, copy bank, tech stack canon — and routes design work through five named specialist agents. Two identities ship in the box; new ones drop in via a template. Works the same on any machine where the plugin is installed.

## The Two Identities

| Identity | Slug | Default for |
|---|---|---|
| **Modern Architect** | `modern-architect` | Personal projects, side work, products under Antonio's own name. Linen `#F7F6F2`, Chimney Smoke `#2C2F33`, Blue Agave `#5A727A` accent. |
| **Reliance Architecture** | `reliance-architecture` | Reliance Architecture firm — client portals, BIM viewers, AEC plugins, internal tools. White, Neutral Black `#262626`, Reliance Steel `#6B8CA3`, plus four division variants (Public, Liturgical, Residential, Commercial). |

Adoette selects the active identity at session start based on project context. Switch any time with *"Switch to Reliance"* or *"Switch to Modern Architect."*

## The Five Agents

| Agent | Origin | Role | Invoke with |
|---|---|---|---|
| **Adoette** | Kiowa — "big tree" | Master coordinator. Selects identity, loads the covenant, routes to specialists. | `adoette-master` |
| **Aditsan** | Navajo — "listener" | Design critique. Severity-tagged review against the active identity. | `aditsan-design-critique` |
| **Atsila** | Cherokee — "fire" | Component generation. Production React/TS using active identity's tokens. | `atsila-component-generation` |
| **Aiyana** | Cherokee — "eternal blossom" | Project kickoff. Full UI/UX brief tied to identity + platform. | `aiyana-project-kickoff` |
| **Anaba** | Navajo — "she returns from war" | Accessibility audit. WCAG 2.1 AA + resilience + thumb zone, against the active identity. | `anaba-accessibility-audit` |

## Installation

### Claude Code (any machine)

```bash
claude plugin install ./ui-ux-architect.plugin
```

### Cowork (desktop app)

Open the `.plugin` file in Cowork → click **Install** in the preview card.

After install, the five skills appear in your session and route automatically.

## How to Use

### Start every session
```
Adoette, load the covenant. This is a Reliance Architecture client portal.
```

Or for personal work:
```
Adoette, load Modern Architect. I'm working on the Thermomix sync app.
```

### Then route by intent

- **"Review this client-portal mockup"** → Aditsan auto-invokes, critiques against Reliance Architecture
- **"Build me a project header component"** → Atsila auto-invokes, uses Montserrat + Reliance Steel
- **"Kickoff brief for the Liturgical division's project intake tool"** → Aiyana auto-invokes, applies Liturgical Gold variant
- **"Is the BIM viewer accessible?"** → Anaba auto-invokes, audits against Reliance contrast pairs

If intent is ambiguous, Adoette asks one sharp clarifying question.

### Switching identity mid-session
```
Switch to Modern Architect — I'm pivoting to my personal sweeper utility.
```

## Adding a New Identity

1. Open `skills/adoette-master/references/identities/_TEMPLATE.md`.
2. Save as `<your-slug>.md` (kebab-case).
3. Fill every section — palette, type, geometry, motion, CSS variables.
4. Drop logo assets (if any) into `skills/adoette-master/assets/<your-slug>/`.
5. Add an entry to `skills/adoette-master/references/identities/_index.md`.
6. Repackage the plugin (or work from the unpacked source tree).

## What's Inside

```
ui-ux-architect/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── adoette-master/
│   │   ├── SKILL.md
│   │   ├── references/
│   │   │   ├── identities/
│   │   │   │   ├── _index.md
│   │   │   │   ├── _TEMPLATE.md
│   │   │   │   ├── modern-architect.md
│   │   │   │   └── reliance-architecture.md
│   │   │   ├── platform-blueprints.md
│   │   │   ├── component-specs.md
│   │   │   ├── tech-stack-canon.md
│   │   │   └── copy-bank.md
│   │   ├── examples/
│   │   │   ├── 01_example-critique.md
│   │   │   ├── 02_example-component.md
│   │   │   ├── 03_example-kickoff.md
│   │   │   └── 04_example-audit.md
│   │   └── assets/
│   │       ├── design-system-showcase.html
│   │       └── reliance-architecture/
│   │           ├── README.md
│   │           ├── RA-Icon-Color.svg       (Reliance Steel #6B8CA3)
│   │           ├── RA-Icon-Black.svg
│   │           ├── RA-Icon-White.svg
│   │           ├── RA-Icon-Public.svg      (Public #DE614A)
│   │           ├── RA-Icon-Liturgical.svg  (Liturgical #D9AB33)
│   │           ├── RA-Icon-Residential.svg (Residential #6BA391)
│   │           ├── RA-Icon-Commercial.svg  (Commercial #B46C42)
│   │           └── Reliance Architecture Style Guide.pdf
│   ├── aditsan-design-critique/
│   ├── atsila-component-generation/
│   ├── aiyana-project-kickoff/
│   └── anaba-accessibility-audit/
└── README.md
```

The four specialist skills all cite shared references in `adoette-master/`.

## Universal Rules (Apply to All Identities)

These never bend, regardless of which identity is loaded:

- WCAG 2.1 AA contrast minimums
- 8pt grid for spacing
- Animation ≤ 200ms, ease-out
- Touch targets ≥ 44×44px
- No tooltips for primary actions
- Skeleton screens for loading
- Localized, actionable error states
- State the platform AND identity before designing

Everything else — colors, type family, radius, borders, motion preferences — is identity-specific.

## Tech Stack Routing

- **UI / front-end:** TypeScript + React (Next.js, React Native)
- **Backend / API:** Python (FastAPI)
- **Performance:** Rust via PyO3 FFI
- **Server orchestration:** Go
- **AEC plugins (ArchiCAD, Bluebeam, Revit, AutoCAD):** C# / .NET

## Visual References

- `skills/adoette-master/assets/design-system-showcase.html` — Modern Architect single-file visual reference
- `skills/adoette-master/assets/reliance-architecture/Reliance Architecture Style Guide.pdf` — official Reliance brand spec from Left Hand Design

## Versioning

- `0.1.0` — first portable package (Modern Architect only)
- `0.2.0` — Reliance Architecture identity added, identity template + index, asset bundle
- Bump version in `.claude-plugin/plugin.json` when shipping changes.

## License

MIT — Antonio Naylor.
