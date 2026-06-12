# Identity Index

> Registry of all design identities available in this plugin. Adoette reads this first to decide which identity to load.

## Active Identities

| Slug | Name | Default for | File |
|---|---|---|---|
| `modern-architect` | Modern Architect | Antonio's personal projects, side work, products shipped under his own name | `modern-architect.md` |
| `reliance-architecture` | Reliance Architecture | Reliance Architecture firm work — client portals, BIM viewers, AEC plugins, internal tooling | `reliance-architecture.md` |

## Default Selection Rules

When the active identity is not explicitly stated, Adoette decides in this order:

1. **Explicit declaration** — User says "use Reliance Architecture" or "this is a firm project" → load `reliance-architecture`.
2. **Folder / project name signal** — Project path contains `reliance`, `RA-`, `firm-`, `client-portal`, `bim`, or similar → load `reliance-architecture`.
3. **Surface type signal** — User is building a client portal, AEC plugin, or anything that will surface the firm's brand to a client → load `reliance-architecture`.
4. **Personal signal** — Project is for Antonio's own use, a side product, a personal automation, or a tool for his home setup → load `modern-architect`.
5. **Ambiguous** — Ask one sharp clarifying question: *"Reliance Architecture project, or personal?"*

## Adding a New Identity

1. Copy `_TEMPLATE.md` to `<your-slug>.md`.
2. Fill every section.
3. If the brand has logo assets, drop them into `../assets/<your-slug>/` and add a `README.md` describing what's bundled vs. what lives elsewhere.
4. Add an entry to the "Active Identities" table above.
5. Update Adoette's SKILL.md routing rules if the new identity needs special triggers.

## Retiring an Identity

Move it to an `_archive/` subfolder rather than deleting — there may be projects in maintenance that still target the older spec.
