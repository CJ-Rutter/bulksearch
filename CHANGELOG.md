# Changelog

All notable changes to BulkSearch are documented here. Format: [Keep a Changelog](https://keepachangelog.com/). Versioning: [SemVer](https://semver.org/).

---

## [Unreleased]

### Planned
- Highlight search matches in results
- Keyboard nav (arrow keys to move between rows, Enter to copy part #)
- Recent searches history (localStorage)
- Export filtered results to CSV
- Iterate on `cleanDescription` once real messy cases surface (acronym preservation, common abbreviations)

---

## [0.13.1] — 2026-05-27

### Added
- **Machine-fitment sub-line on QC coupler cards.** Each QC card now shows a small dimmed line below the head with the mini-excavator class the coupler fits: `QC27` → "Fits 15–50 sized mini excavators", `QC30` → "Fits 80–90 sized mini excavators". Dashed underline separates it from the first size row. Sourced from a small `QC_FITMENT` lookup in the renderer (not the CSV) — domain knowledge that doesn't live in the parts data. Future coupler sizes just need an entry in the lookup to surface their own fitment line.

---

## [0.13.0] — 2026-05-27

### Added
- **Core Drill Bits panel on the Bulk Cheat Sheet.** Fourth featured section, matched on `CORE DRILL BIT NN"` (handles whole inches like `10"` and mixed fractions like `1-1/2"`, `2-1/2"`). Renders as a single full-width card listing every diameter; on desktop the sizes flow into two visual columns so the 15-entry list stays compact. Lets a coordinator land on "I need a 4-inch core bit" without scrolling the flat table.

### Notes
- Core drill bits are single-axis (diameter only — no length, no type), so they break from the card-per-discriminator pattern used by the bucket and auger panels. Future single-axis categories can reuse the `.qc-card-columns` modifier for the same compact two-column layout.

---

## [0.12.0] — 2026-05-27

### Added
- **Auger extensions in the auger panel.** Extension auger bits (`EXTENSION AUGER BIT ... NN" LENGTH` — shaft only, no flighting) used to fall through to the flat table. They now render as a trailing "Extensions" card inside the Auger Bits panel, grouped by length, so a coordinator pulling a 4-foot bit can grab the matching extension without leaving the section. Panel title renamed to "Auger Bits & Extensions — by Size · Length".

### Changed
- **Length displayed in feet.** Auger panel now shows length as `4'` / `2'` instead of `48"` / `24"` — matches how dispatchers and techs actually talk about auger lengths. Bit diameter (size) stays in inches per industry convention.

---

## [0.11.1] — 2026-05-27

### Changed
- **Cheat sheet panel headers.** Section titles ("QC Coupler Buckets", "Excavator Buckets — by Pin Diameter", "Auger Bits — by Size · Length") are now panel headers — 20px monospace, bold, uppercase, centered, accent-colored, with top/bottom accent rules and a tinted background — so the three (and future) featured groups read as distinct panels instead of quiet subheaders. Per-section separator firmed up from a 1px dashed rule to a 2px solid one. New categories added later inherit the same treatment automatically (single `.qc-featured-title` rule).

---

## [0.11.0] — 2026-05-27

### Added
- **Auger Bits featured section on the Bulk Cheat Sheet.** Third card grid below the QC and pin-diameter bucket trees, scoped to bulk auger bit rows. Same card layout, grouped by **diameter → length** (e.g. `6" Bit` card → `48"` row → part #). Lets a coordinator land on "I need a 6-inch by 4-foot auger bit" without scrolling the flat table. Extension augers (no diameter, shaft-only) stay in the flat table.

---

## [0.10.0] — 2026-05-27

### Added
- **Excavator buckets — by Pin Diameter** featured section on the Bulk Cheat Sheet. Mirror of the QC27/QC30 card tree but keyed on pin diameter (the bushing size that determines which excavator class the bucket fits) instead of coupler code. Same Dig (toothed) / Clean (smooth, incl. ditching) split, same width sub-rows, same capacity + bin annotation. Lets a coordinator land on "I need a 24-inch dig bucket for an 80mm pin machine" without scrolling the flat table.
- **mm → inches conversion on pin labels.** Source descriptions quote pin diameters in mm (45/50/65/70/80/90); the cheat sheet header renders the inch equivalent rounded to the nearest 1/16" and reduced (e.g. `80mm` → `3-1/8" Pin`, `65mm` → `2-9/16" Pin`) so it reads naturally for the shop floor.

### Notes
- The non-QC bucket parser (`parseBucket`) requires both a width (`BUCKET NN"`) and a pin token (`NNMM`) in the source description; rows missing either fall through to the flat table.

---

## [0.9.0] — 2026-05-27

### Added
- **Clickable version chip → recent changelog.** The `v0.9.0` badge in the header is now a button. Clicking it opens a centered modal that lazy-fetches `CHANGELOG.md`, parses out the `[Unreleased]` block plus the five most recent versions, and renders them with light markdown formatting (version headings, section subheaders, bullet lists, inline `code` and **bold**). Closes on the × button, backdrop click, or Escape. Falls back to a "View on GitHub →" link when the fetch fails (e.g. `file://` runs).
- **Click-to-copy on Bulk Cheat Sheet part #s.** Cheat-sheet rows and the QC bucket cards now use the same `.part-badge` markup as the main search table — accent-bordered chip, copy-icon affordance on hover, success flash + "COPIED" tag, clipboard fallback for non-secure contexts. Copy click delegation moved from the search `<tbody>` to `document` so a single handler covers all three surfaces (main table, cheat sheet table, QC tree).

---

## [0.8.0] — 2026-05-15

### Added
- **QC27 / QC30 featured section on Bulk Cheat Sheet.** Quick-coupler excavator buckets get pulled out of the flat table and rendered as a structured tree at the top: `QC27 Buckets` / `QC30 Buckets` → bucket width (12", 18", 24", 36", 48") → Dig (toothed edge) / Clean (smooth, including ditching buckets) → part number with capacity range and bin location. Lets a coordinator land on "I need a 24-inch QC30 dig bucket" in seconds without scrolling the whole sheet. The rest of the bulk items continue below in the existing compact table.

---

## [0.7.0] — 2026-05-15

### Added
- **Bulk Cheat Sheet tab.** New top-level view alongside Search, scoped to bulk items only (MFR starts with `BULK`). Compact 3-column table — Part # / Description / Bin Location — sorted by Bin then Part #, with a thin divider between bin groups so the eye can chunk. Search box is reused and scoped to bulk rows while the tab is active; toggles / MFR filter / sort controls hide for that view.
- **Description normalization** (`cleanDescription`). Title-cases shouty source data, collapses internal whitespace, and spaces out common unit suffixes (`33LB` → `33 lb`). Conservative whitelist of units to avoid breaking model numbers like `UL32A`. First-pass implementation; will iterate as messy real-world cases surface.

---

## [0.6.2] — 2026-05-14

### Fixed
- **Part # column overlap, take two.** v0.6.1 forced `.part-badge` back to `display: inline` but missed that the parent `.col-part` cell has `white-space: nowrap` set globally for the on-screen layout. `nowrap` forbids wrapping at the cell level, so `word-break: break-all` never got a chance to fire. Print CSS now explicitly overrides `white-space` to `normal` on `.col-part`, `.part-badge`, and `.part-text` (plus keeps the wrap rules from before). Long part numbers now actually wrap to a second line inside the column.

---

## [0.6.1] — 2026-05-14

### Fixed
- **Part # column overlapping Description in print.** Long part numbers (`SUIME24COB-WR1`, `48120X2-3135`, etc.) were rendering on a single line and overflowing into the next column. Root cause: `.part-badge` is `display: inline-flex` on screen, which creates a flex layout context that doesn't honor parent `word-break` rules. Print CSS now forces it back to plain inline flow so the cell's fixed column width + `break-all` can actually constrain the part text and wrap it to a second line.

---

## [0.6.0] — 2026-05-14

### Added
- **Update-available banner.** When a newer version is published, an open tab notices and surfaces a small bottom-right banner: "**v0.6.1** available (you're on v0.6.0)" with a Reload button and an × dismiss. Dismissals stick per-version (localStorage), so the same banner doesn't nag — it'll re-show when the next version ships.
- Check fires 60s after load, on tab-focus (so coworkers who leave the tab open across days see the prompt the moment they come back), and every 10 minutes as a backstop.
- `cache: 'no-store'` + cache-buster query on the fetch so the browser's HTML cache can't mask a real update.
- Robust against offline, `file://` runs, and version-extraction failure: silently no-ops, never breaks the app.

### Notes
- Pure DOM/fetch — no service worker. Keeps the "open the HTML and it works" property intact for local dev / air-gapped use.
- Version comparison is numeric per segment (so `0.6.10` > `0.6.2` works correctly).

---

## [0.5.0] — 2026-05-14

### Changed
- **Ships blank.** The embedded `INVENTORY` array is now empty — BulkSearch is a generic search-shell that requires a CSV upload to do anything. Removes ~252KB of ES-specific parts data from the bundle and makes the repo safe to publish.
- **"Reset" → "Clear data."** With no built-in baseline, the button now wipes whatever CSV is loaded (and its localStorage cache) back to the empty state. Icon swapped to a trash glyph.
- **Empty state is now contextual.** No data loaded → friendly "Upload a CSV to get started" with a pointer at the Upload CSV button. No matches in filter → original "/ / /" empty-state design.
- **Header strip cleaned up** — removed the hard-coded `2026-04-22` snapshot date; the date now only appears when a user-uploaded CSV is loaded.

### Notes
- Repo flipped to **public** in this release. With the data stripped, the tool itself is a generic parts-search utility that's fine to share. The data your coworkers load stays in their browser — single-page app, no backend.
- Live URL: https://cj-rutter.github.io/bulksearch/ (served via GitHub Pages from the `main` branch root).

---

## [0.4.2] — 2026-05-14

### Fixed
- **Qty + Cost columns getting clipped in print.** Without an explicit column layout, browsers let Description and Bin balloon to fit content, squeezing the right-side numeric columns down to a few characters or off the page entirely. Print table now uses `table-layout: fixed` with allocated percentages (Part 13% / Description 32% / Make 16% / Bin 19% / Qty 8% / Cost 12%), reserving room for the right edge.
- Tightened page margin from 0.5in to 0.4in to recover ~0.4in of usable width.
- Long descriptions, makes, and part numbers now wrap inside the cell (via `word-break: break-word` / `overflow-wrap: anywhere`) instead of forcing the column wider than its allotment.

---

## [0.4.1] — 2026-05-14

### Fixed
- **Bin Location column cutoff.** Long bin values (e.g. `"Parts Room Leaning on Wall by Batteries"` — 39 chars) were forcing the column to nowrap, which pushed adjacent columns or overflowed the table on screen and clipped at the page edge in print. The chip now wraps to multiple lines inside the cell, the column is capped at 220px on screen / 1.6in on print, and short codes like `AA1B` still render compact on a single line.

---

## [0.4.0] — 2026-05-14

### Added
- **Print button** in the data-actions row, plus a comprehensive `@media print` stylesheet. Click Print (or hit Ctrl/Cmd+P) and the paper version drops the dark-UI chrome, renders a clean black-on-white table with repeating column headers across pages, and leads with a summary block: title + version, dataset name, current row count, print date, and a one-line "filters applied" recap (search term, make, in-stock, bulk mode, sort).
- Rows are kept together across page breaks; part numbers stay monospace and bold; bin tags flatten to plain bordered chips; numeric columns right-aligned with tabular numerals.
- `updatePrintSummary()` also runs on `beforeprint`, so browser-initiated prints (keyboard shortcut, browser menu) get the same context block as the button-triggered print.

---

## [0.3.0] — 2026-05-14

### Added
- Version chip in the header next to the BulkSearch wordmark, in the industrial accent palette.
- "Feedback" button in the header-meta row — opens a mailto to cj.rutter@equipmentshare.com with the subject prefilled to identify the tool + version.

### Notes
- Matches the ES-tool UI convention established on RentalPulse: every work-facing repo needs a version badge near the title and a Feedback button routing to the maintainer.

---

## [0.2.0] — Branding + multi-data

### Added
- CSV upload — swap datasets without editing the file
- Manufacturer filter dropdown (rebuilds when dataset changes)
- Bulk filter segmented control: All / Bulk only / Hide bulk
- Light/dark theme toggle
- Reset filters button

### Changed
- Renamed from "Core Solutions — Parts Search" to "BulkSearch"
- Removed Marysville-specific tagline (tool is now portable)
- Brand mark changed from "CS" to "[B]"

## [0.1.0] — Initial deployment

### Added
- Single-file HTML parts search
- Instant filtering by part #, description, MFR
- Part # column as the prominent identifier
- In-stock toggle
- ~2,100 inventory items hard-coded
