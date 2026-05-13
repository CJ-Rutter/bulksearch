# BulkSearch

Fast client-side parts inventory search. Drop in a CSV inventory export, type a partial part number or description, and get filtered results instantly. Part # is the star — front-and-center, monospace, copyable.

**Audience:** Coordinators, parts/service techs, anyone looking up a part across thousands of inventory items.

**Built by:** CJ Rutter — Dispatch, EquipmentShare Marysville Branch.

---

## What it does

- **Instant search** — Type-as-you-go filtering. Searches part #, description, make/model.
- **Manufacturer filter** — Dropdown narrows to a single MFR.
- **In-stock toggle** — Hide zero-qty items.
- **Bulk filter** — Three-way segmented control: All / Bulk only / Hide bulk. Catches the ~100 "BULK*" pseudo-items.
- **CSV upload** — Drop a new export and the whole tool refreshes against the new dataset.
- **Theme toggle** — Light/dark.
- **Sortable columns** — Part #, qty, MFR, cost.

## Stack

- Single-file HTML. Vanilla JS. No build step. Open it and use it.

## Running locally

```bash
git clone <this repo>
cd bulksearch
# open index.html in your browser
```

For a different inventory, click the **Upload CSV** button and pick your file. Expected columns: `PART #`, `ITEM DESCRIPTION`, `MFR`, `AVAILABLE QTY`, `COST`, `NOTE`. Other columns are ignored.

## Working with Claude Code

```
Read CLAUDE.md and CHANGELOG.md, then we'll work on [feature].
```

## Status

In use at Marysville against a ~2,100-item inventory.
