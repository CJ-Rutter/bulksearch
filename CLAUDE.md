# BulkSearch — Claude Code Context

> Read this first.

## Project at a glance

- **What:** Client-side parts inventory search. Instant filtering across thousands of parts by part #, description, MFR. Part # is the most prominent column.
- **Audience:** Coordinators, parts/service techs, dispatch.
- **Author:** CJ Rutter (Dispatch, Marysville).
- **Tech:** Single `index.html`. Vanilla JS. No build, no dependencies, no backend.

## Architecture

- One HTML file. Inventory is embedded as a JS array (`const INVENTORY = [...]`) AND/OR loaded via CSV upload.
- `currentData` is the working dataset — gets replaced when a new CSV is uploaded.
- Filtering happens in a single loop over `currentData` driven by:
  - `searchInput.value` — substring match against part #, description, MFR
  - `mfrFilter.value` — exact MFR match
  - `inStockOnly.checked` — `qty > 0`
  - `bulkMode` — "all" / "bulk-only" / "hide-bulk"
- Re-renders on any filter change. Fast enough at 2k–5k rows; if it ever needs to handle 50k+ rows, look at debouncing and virtualized rendering.

## Conventions

- **Aesthetic:** Industrial/utilitarian. Dark UI by default. Monospace for part numbers (they're the star).
- **Brand mark:** `[B]` in a square in the top-left. Title: "BulkSearch". Created-by tag: "CJ Rutter".
- **Color tokens:** Use CSS variables defined in `:root` — never hard-code colors mid-file.
- **Filter reset on dataset swap:** When a CSV is uploaded or "Reset" is hit, ALL filters snap back to defaults. This is intentional — new data, fresh state.

## Things to avoid

- Don't add a build step. Single-file is a feature.
- Don't add a backend. Don't add user accounts.
- Don't bundle real customer-specific data with the repo. Sample CSV in `data/` should be sanitized.
- Don't break the "Part # is the most prominent column" rule. Description and MFR are supporting.
- Don't auto-sort by anything other than part # ascending unless the user explicitly clicks a column header.

## Where to look

- `index.html` — the app
- `data/` — sample CSV(s)
- `docs/csv-format.md` — expected CSV columns and quirks
- `docs/filter-logic.md` — how filters combine
- `CHANGELOG.md` — version history

## Working style

- The file is ~1500 lines but well-structured. Use grep heavily before editing — don't view the whole thing.
- When changing filter logic, update `docs/filter-logic.md` in the same commit.
- After CSS changes, eyeball both light and dark themes.
