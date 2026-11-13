# report-formatter (БпАК Formatter) — formats UAV strike reports for operators

## Stack & layout
- Vanilla JavaScript, ES modules. Tests: Vitest. Map: Leaflet.
- Ships as a single encrypted HTML file to GitHub Pages, from two repos.
- No runtime dependencies.

## Commands
- Install: `<...>`                 # unverified — copy the real command
- Test: `<vitest>`                # unverified
- Build / bundle: `<...>`         # unverified

## Rules
- Patch in place; do not rewrite working modules.
- Extract a helper when the same logic appears in 2+ places (e.g. match and geocoding helpers).
- Prefer data tables (alias maps) over if/else chains.
- Keep zero runtime dependencies.

## Hazards
- Reports carry invisible characters. Strip U+200E/200F/200B/FEFF in `clean()` before parsing.
- Munition token: trailing 1–4 is a quantity; ≥5 is part of the name (e.g. МОА-900).
- All text and filenames are UTF-8; filenames may be Cyrillic. Set encoding explicitly.
- Every parser fix gets a regression fixture from a real report. Add the fixture first.

## Docs
- `docs/agent/uav-reports.md` — read before any parser, formatter, or munition change.
