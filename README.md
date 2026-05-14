# BulkSearch

Fast client-side parts inventory search. **Ships blank** — upload your own CSV and the tool reads, indexes, and searches it in your browser. No backend, no data ever leaves the page.

**Live demo:** https://cj-rutter.github.io/bulksearch/

**Audience:** Anyone looking up a part across thousands of inventory items — coordinators, parts/service techs, dispatch.

**Built by:** CJ Rutter.

---

## What it does

- **Instant search** — type-as-you-go filtering across part #, description, make/model, bin location, notes.
- **Manufacturer filter** — dropdown narrows to a single MFR (rebuilt from whatever CSV you upload).
- **In-stock toggle** — hide zero-qty items.
- **Bulk filter** — three-way segmented control: All / Bulk only / Hide bulk. Catches `BULK*` pseudo-items.
- **Match-all-words toggle** — for tighter multi-term searches.
- **CSV upload** — drag-and-drop or click. Browser stores it locally so it survives page reloads.
- **Print** — paper-friendly layout with the current filter summary at the top, column widths locked, headers repeat on each page.
- **Theme toggle** — light / dark.
- **Sortable columns** — Part #, qty, MFR, cost.

## Stack

Single-file HTML. Vanilla JS. No build step, no dependencies. Open `index.html` directly or hit the live demo URL.

## CSV format

Required columns (header row, case-insensitive, common variations are auto-detected):

| Column        | Aliases accepted                              |
|---------------|------------------------------------------------|
| Part #        | `part`, `part number`, `part #`                |
| Description   | `description`, `item description`, `desc`      |
| Make          | `make`, `mfr`, `manufacturer`, `brand`         |
| Bin Location  | `bin`, `bin location`, `location`              |
| Qty Avail.    | `qty`, `available qty`, `quantity`             |
| Cost          | `cost`, `price`                                |

A `note` / `notes` column is also picked up if present. Other columns are ignored.

See `docs/csv-format.md` for full details and edge cases.

## Sharing

- **For coworkers who just need to use it:** send them the live demo URL above. They drop their own CSV; nothing's uploaded anywhere — everything runs in their browser.
- **For local dev or air-gapped use:** clone the repo and open `index.html` directly.

## Privacy

BulkSearch is a static page. Whatever CSV you upload stays on your machine — there is no server, no analytics, no telemetry. Browser localStorage holds the last-uploaded CSV so you don't have to re-drop it every page load; clearing the browser's site data wipes it.

## Working with Claude Code

```
Read CLAUDE.md and CHANGELOG.md, then we'll work on [feature].
```
