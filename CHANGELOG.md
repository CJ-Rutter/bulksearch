# Changelog

All notable changes to BulkSearch are documented here. Format: [Keep a Changelog](https://keepachangelog.com/). Versioning: [SemVer](https://semver.org/).

---

## [Unreleased]

### Planned
- Highlight search matches in results
- Keyboard nav (arrow keys to move between rows, Enter to copy part #)
- Recent searches history (localStorage)
- Export filtered results to CSV

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
