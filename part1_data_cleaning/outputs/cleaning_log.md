# Data Cleaning Log — Part 1: Business Data Cleaning, Validation & Excel Reporting

**Dataset:** raw_orders.xlsx  
**Cleaned Output:** cleaned_orders.xlsx  
**Total Raw Records:** 932  
**Total Records After Cleaning:** 912  

---

## 1. Issues Found

| # | Issue | Count | Severity |
|---|-------|-------|----------|
| 1 | Exact duplicate rows | 20 | High |
| 2 | Duplicate order_ids with conflicting data | 12 unique IDs | Medium |
| 3 | Missing `region` values | 26 | Medium |
| 4 | Missing `ship_mode` values | 22 | Medium |
| 5 | Missing `discount` values | 26 | Medium |
| 6 | Negative discount values | 16 | High |
| 7 | Ship date before order date | 94 | High |
| 8 | Inconsistent date formats (7+ formats) | All rows | High |
| 9 | Inconsistent text casing (e.g., NORTH, north, North) | Multiple cols | Medium |
| 10 | Extra whitespace in text fields | Multiple cols | Low |
| 11 | Sales/calculated_sales mismatch | 62 | Medium |
| 12 | Cancelled/Returned/Failed records mixed with Completed | 310 | Medium |

---

## 2. Cleaning Actions Performed

### Task 1 — Preserve Raw Data
- `raw_orders.xlsx` was kept completely unchanged.
- All cleaning was done in a separate file: `cleaned_orders.xlsx`.

### Task 2 — Text Field Cleaning
Applied to: `customer_name`, `segment`, `region`, `state`, `city`, `category`, `sub_category`, `ship_mode`, `payment_status`, `order_status`
- Stripped leading/trailing whitespace using `.str.strip()`
- Replaced multiple internal spaces with single space using regex `\s+`
- Standardized casing to Title Case (e.g., `NORTH` → `North`, `consumer` → `Consumer`)
- Specific corrections:
  - `Small  Business` → `Small Business`
  - `Standard  Class` → `Standard Class`

### Task 3 — Date Cleaning
- Dates existed in 7+ mixed formats: `DD Mon YYYY`, `MM/DD/YYYY`, `DD-MM-YYYY`, `YYYY-MM-DD`, `DD Mon YYYY`, etc.
- Used Python `dateutil.parser` with `pandas.to_datetime` fallback to parse all dates.
- All dates standardized to `YYYY-MM-DD` format in the output file.
- Created `shipping_delay_days` column: `ship_date - order_date` (in days).
- Records where `shipping_delay_days < 0` flagged as `ship_before_order`.

### Task 4 — Duplicate Handling
- **Exact duplicates (20 rows):** Removed using `df.drop_duplicates()`. Kept first occurrence.
- **Conflicting order_ids (12 unique IDs, ~32 rows):** All records kept but flagged with `conflicting_duplicate` in `data_quality_flag`. Not silently deleted.

### Task 5 — Business Rules Applied

| Rule | Action Taken |
|------|-------------|
| Missing `region` | Filled as `Unknown`; flagged as `warning` |
| Missing `ship_mode` | Filled as `Unknown`; flagged as `warning` |
| Missing `discount` | Treated as `0` when `quantity` and `unit_price` are valid |
| Negative discount | Flagged as `invalid` in `data_quality_flag` |
| Cancelled orders | Excluded from completed sales pivot summaries |
| Failed payment orders | Excluded from completed sales pivot summaries |
| Refunded orders | Summarized separately in pivot (Issues By Region sheet) |
| Ship date before order date | Flagged as `invalid` in `data_quality_flag` |

### Task 6 — Calculated Columns Added

| Column | Formula Logic |
|--------|-------------|
| `cleaned_discount` | Original discount; missing → 0 if sales fields valid |
| `calculated_sales` | `quantity × unit_price × (1 − cleaned_discount)` |
| `calculated_profit` | `calculated_sales − cost` |
| `profit_margin` | `calculated_profit / calculated_sales` |
| `shipping_delay_days` | `ship_date − order_date` in days |
| `order_month` | Month number extracted from `order_date` |
| `order_year` | Year extracted from `order_date` |
| `data_quality_flag` | `clean` / `warning` / `invalid` based on rules above |

---

## 3. Records Removed

| Reason | Count |
|--------|-------|
| Exact duplicate rows | 20 |
| **Total removed** | **20** |

---

## 4. Records Flagged

| Flag | Count | Reason |
|------|-------|--------|
| `clean` | 500 | No issues found |
| `warning` | 284 | Missing region/ship_mode; non-completed status |
| `invalid` | 128 | Negative discount; ship before order; conflicting dup ID |

---

## 5. Assumptions Made

1. **Date parsing:** When a date like `03/12/2024` was ambiguous (MM/DD vs DD/MM), Python's `pd.to_datetime` default (MM/DD/YYYY) was applied. Dates matching ISO format (`YYYY-MM-DD`) were parsed as-is.
2. **Missing discount:** Treated as 0 only when `quantity`, `unit_price`, and `sales` fields were non-null. If sales field was also missing, the record was flagged.
3. **Conflicting duplicates:** Defined as records with the same `order_id` but different values in at least one other column (after removing exact duplicates). All kept and flagged.
4. **Segment "Small Business":** The raw data contained entries like `Small  Business` (double space). These were standardized to `Small Business`. No data was merged or dropped.
5. **Sales mismatch:** The original `sales` column was preserved. A new `calculated_sales` column was added with the correct formula. The discrepancy is noted but not auto-corrected in the original column.
6. **Cancelled/Returned orders:** These were excluded from completed sales pivot summaries but kept in the cleaned dataset with appropriate flags.

---

## 6. Limitations

- Date parsing is best-effort; ambiguous dates (e.g., `03/04/2024`) may be misinterpreted.
- Duplicate order_id conflicts were flagged but not auto-resolved — manual review recommended.
- Sales mismatches between `sales` and `calculated_sales` columns were not auto-corrected in `sales`; both columns coexist.
- Screenshots were generated from the Python-created Excel files and may not match a native Excel rendered view exactly.
- No geolocation or product catalog validation was performed (e.g., confirming city-state-region mapping).
