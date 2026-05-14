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
