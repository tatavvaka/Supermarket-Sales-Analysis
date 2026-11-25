# Data Quality & Preparation Notes

## Dataset scope

- Source worksheet: `sources`
- Rows: 10,076
- Columns: 24 (21 original fields + 3 prepared fields)
- Order date range: 3 January 2014 – 30 December 2017
- Exact full-row duplicates: 0
- Unique `order_id`: 5,009

## Source missingness and prepared fields

| Field | Missing in source | Prepared field | Missing after preparation |
|---|---:|---|---:|
| `tanggal_pengiriman` | 315 | `clean_tanggal_pengiriman` | 0 |
| `kota` | 314 | `clean_kota` | 0 |
| `kode_pos` | 315 | `clean_kode_pos` | 0 |

## Preparation decisions

1. Duplicate checking was performed against the 21 original source columns; the three `clean_` fields were not used as duplicate-check columns.
2. Missing `clean_tanggal_pengiriman` values were filled with `tanggal_pemesanan`. Ini adalah asumsi untuk melengkapi working table, bukan actual shipment timestamp.
3. Missing city values were mapped using the province-to-city reference table. Whitespace and capitalization were standardized.
4. Missing postal codes were mapped using the province-to-postal-code reference table and stored as five-character identifiers.
5. Sales values were checked for zero values. Negative profit values were retained because they represent losses rather than automatically invalid records.

## Additional audit observations

- `row_id` has 9,994 distinct values across 10,076 rows; therefore, it is not unique.
- `order_id` has 5,009 distinct values. Repeated order IDs are expected for multi-line orders and should not be treated as duplicate records by themselves.
- `keuntungan` contains 1,885 negative values and 65 zero values.
- `penjualan` contains 0 zero values.
- All prepared city and postal-code fields are populated in the supplied export.

## Interpretation caution

Prepared shipping dates avoid nulls in the working table, but they are not verified delivery timestamps. Actual delivery lead-time claims should use only records with original shipping dates. The original `tanggal_pengiriman` column remains available for traceability.
