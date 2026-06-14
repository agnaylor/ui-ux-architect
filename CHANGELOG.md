# Changelog

All notable changes to ui-ux-architect are recorded here.
This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.1] — 2026-06-13

### Changed
- README install instructions now use the GitHub marketplace flow (`/plugin marketplace add agnaylor/ui-ux-architect`) instead of the legacy local-file install.
- Added canonical-source URL (`https://github.com/agnaylor/ui-ux-architect`) at the top of the README.
- Added direct-clone install path (`git clone … ~/.claude/plugins/architect-tools`) as an alternative.
- `plugin.json` now declares `homepage` and `repository` fields pointing at the GitHub repo.

### Added
- This `CHANGELOG.md`.

## [0.2.0] — 2026-06-13

### Added
- **Reliance Architecture identity** sourced from the official 2021 Style Guide (Left Hand Design / Beau Morrow).
  - White / Neutral Black `#262626` / Reliance Steel `#6B8CA3` foundation.
  - Montserrat type stack (SemiBold headlines, ALL CAPS subheads, Regular body).
  - Four division variants: Public `#DE614A`, Liturgical `#D9AB33`, Residential `#6BA391`, Commercial `#B46C42`.
  - Logo SVG assets bundled (Color, Black, White, plus all four divisions).
  - Style Guide PDF bundled.
- **Identity template** (`_TEMPLATE.md`) for adding new brands.
- **Identity index** (`_index.md`) — registry of available identities + selection rules.
- **Marketplace manifest** (`.claude-plugin/marketplace.json`) — turns the plugin into a single-plugin marketplace named `architect-tools`.

### Changed
- Adoette skill now selects the active identity at session start instead of hard-coding Modern Architect.
- All four specialist skills (Aditsan, Atsila, Aiyana, Anaba) reference the active identity rather than a fixed token file.
- Aiyana kickoff brief format now declares `Identity` alongside `Platform`.
- Platform-blueprints deepened the Desktop/AEC section with ArchiCAD / Revit / Bluebeam / AutoCAD theming, ribbon UI conventions, WPF patterns, and AEC interaction patterns.

## [0.1.0] — 2026-06-13

### Added
- Initial portable package — Modern Architect identity only.
- Five named agents:
  - **Adoette** (Kiowa, "big tree") — master coordinator
  - **Aditsan** (Navajo, "listener") — design critique
  - **Atsila** (Cherokee, "fire") — component generation
  - **Aiyana** (Cherokee, "eternal blossom") — project kickoff
  - **Anaba** (Navajo, "she returns from war") — accessibility audit
- Reference files: design tokens, platform blueprints, component specs, tech stack canon, copy bank.
- Four example outputs matching each specialist's pattern.
- Single-file `design-system-showcase.html` for visual reference.
