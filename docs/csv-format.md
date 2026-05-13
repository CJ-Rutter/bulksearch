# CSV Format — BulkSearch

Loaded only when needed via `@docs/csv-format.md`.

## Expected columns

The CSV parser looks for these column headers (case-insensitive, exact name match):

| Header | Internal field | Required | Notes |
|---|---|---|---|
| `PART #` | `part` | yes | Primary identifier |
| `ITEM DESCRIPTION` | `desc` | yes | |
| `MFR` | `mfr` | yes | Used by manufacturer filter and bulk detection |
| `AVAILABLE QTY` | `qty` | no | Defaults to 0 |
| `COST` | `cost` | no | |
| `NOTE` | `note` | no | |

Any other columns in the source CSV are ignored (`VALUE`, `WAC`, `BIN LOCATION`, `ALLOCATED`, `TOTAL QTY OWNED`, etc).

## Bulk detection

An item is considered "bulk" if its `MFR` (case-insensitive, after trimming) starts with `"BULK"`. The bulk filter uses this rule. Currently ~100 bulk items in the sample dataset (drill core bits, tool steel chisels, buckets, augers, trailers, hoses).

## Known source quirks

- UTF-8 BOM on first column header — parser uses `encoding="utf-8-sig"` equivalent.
- Trailing whitespace on values — always `.trim()` after parsing.
- Quantity sometimes blank (treat as 0).
- Cost sometimes formatted with `$` and commas (`$1,234.56`) — strip non-numeric before parsing.

## Adding a new column

1. Update the parser to read it.
2. Update this doc.
3. Decide whether it gets a column in the rendered table.
4. Bump the minor version in `CHANGELOG.md`.
