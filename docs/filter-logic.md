# Filter Logic — BulkSearch

Loaded only when needed via `@docs/filter-logic.md`.

All filters are AND-combined. An item is shown only if it passes every active filter.

## Filters

### 1. Search (text input)

Substring match (case-insensitive) against:
- `part` (part #)
- `desc` (description)
- `mfr` (manufacturer)

If "multi-word" mode is on (checkbox), each whitespace-separated term in the search must match somewhere — terms can match different fields. Example: searching `"bit core"` matches an item with `desc = "Core drill bit"` even though "bit" and "core" are reversed.

### 2. Manufacturer filter (dropdown)

Exact match against `mfr`. The dropdown is rebuilt from the current dataset's unique manufacturers, sorted alphabetically. Default: "All makes" = no filter.

### 3. In-stock toggle (checkbox)

When on, hide items where `qty <= 0`.

### 4. Bulk filter (segmented control: 3-way)

- **All** (default) — no filter
- **Bulk only** — show only items where `mfr` starts with "BULK"
- **Hide bulk** — hide items where `mfr` starts with "BULK"

### 5. Sort

Independent of the filter chain. Click a column header to sort by that column. Default sort: part # ascending.

## Reset behavior

Clicking **Reset** OR uploading a new CSV resets:
- Search input → empty
- Manufacturer filter → "All makes"
- In-stock toggle → off
- Bulk filter → "All"
- Sort → part # ascending

This is intentional: a new dataset means a fresh start.

## Performance

At ~2,100 rows the filter+render runs in <10ms per keystroke. If the dataset grows past ~10k rows, add input debouncing (200ms) before optimizing further. Past 50k rows, look at virtualized rendering (only DOM-rendering visible rows).
