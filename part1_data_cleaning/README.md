# Part 1: Business Data Cleaning, Validation & Excel Reporting

## 1. Problem Summary

A retail company's order management system exported raw order-level sales data from multiple internal sources. The dataset contained inconsistent text formatting, date format problems, duplicate records, missing values, invalid discounts, calculation mismatches, and order status inconsistencies. The goal was to clean, validate, and document the data, then create summary reports using Excel.

---

## 2. Dataset Description

- **File:** `data/raw_orders.xlsx`
- **Sheet:** `raw_orders`
- **Total Records:** 932 rows, 21 columns
- **Date Range:** 2024–2025
- **Key Fields:** order_id, order_date, ship_date, customer details, product details, financials (quantity, unit_price, discount, sales, cost, profit), payment_status, order_status

---

## 3. Tools Used

- **Python 3** — Data cleaning and processing
  - `pandas` — Data manipulation and analysis
  - `openpyxl` — Excel file creation and formatting
  - `dateutil` — Flexible date parsing
  - `numpy` — Numerical operations
- **Excel** — Final output view and verification

---

## 4. Cleaning Steps Performed

1. **Preserve raw data** — `raw_orders.xlsx` kept unchanged; all cleaning done in `cleaned_orders.xlsx`
2. **Text cleaning** — Trimmed whitespace, standardized casing, fixed double-spaces across 10 columns
3. **Date standardization** — Parsed 7+ mixed date formats into consistent `YYYY-MM-DD` format
4. **Duplicate removal** — Removed 20 exact duplicate rows; flagged 12 conflicting order_id groups
5. **Missing value handling** — Filled missing `region` and `ship_mode` as `"Unknown"`; missing `discount` treated as 0
6. **Business rule enforcement** — Negative discounts flagged; cancelled/failed orders excluded from sales summaries
7. **Calculated columns** — Added 8 new derived columns (see Section 5)
8. **Data quality flags** — Each record classified as `clean`, `warning`, or `invalid`

---

## 5. Business Rules Applied

| Rule | Action |
|------|--------|
| Missing `region` | Filled as `Unknown`, flagged in quality report |
| Missing `ship_mode` | Filled as `Unknown`, flagged in quality report |
| Missing `discount` | Treated as 0 if other sales fields are valid |
| Negative discount | Flagged as `invalid` |
| Discount > 100% | Flagged as `invalid` (none found) |
| Cancelled orders | Excluded from completed sales summaries |
| Failed payments | Excluded from completed sales summaries |
| Refunded orders | Summarized separately in pivot reports |
| Ship date before order date | Flagged as `invalid` |
| Exact duplicate rows | Removed; first occurrence kept |
| Conflicting order_ids | Kept and flagged, not silently deleted |

---

## 6. Summary of Data Quality Issues Found

| Issue | Count |
|-------|-------|
| Exact duplicate rows | 20 |
| Duplicate order_ids (conflicting) | 12 unique IDs |
| Missing `region` | 26 |
| Missing `ship_mode` | 22 |
| Missing `discount` | 26 |
| Negative discounts | 16 |
| Ship date before order date | 94 |
| Sales/calculated_sales mismatch | 62 |
| Text casing/whitespace issues | Widespread |

**Final record counts (after cleaning):**
- Total records: 912
- Clean: 500 (54.8%)
- Warning: 284 (31.1%)
- Invalid: 128 (14.0%)

---

## 7. Summary of Final Pivot Reports (`pivot_summary.xlsx`)

| Sheet | Description |
|-------|-------------|
| Sales By Region | Total sales, profit, order count by region (sorted by sales) |
| Sales By Category | Sales and profit by category and sub-category (sorted by sales) |
| Orders By Ship Mode | Order count and average shipping delay by ship mode |
| Profit By Segment | Profit margin by customer segment (sorted by margin) |
| Issues By Region | Cancelled/returned/failed/refunded orders by region |
| Monthly Sales Trend | Month-by-month sales and profit trend for completed orders |

Sheets "Sales By Region" and "Profit By Segment" include sorting filters.

---

## 8. Key Business Insights

- **West region** leads in total sales volume among completed orders.
- **Technology** category generates the highest revenue overall.
- **Standard Class** is the most used shipping mode.
- **94 records** have ship dates before order dates — a significant data quality issue requiring system-level investigation.
- **16 negative discounts** suggest possible data entry errors in the source system.
- **Cancelled and returned orders** account for over 33% of all records — high return/cancellation rate worth investigating.
- **Corporate** segment shows strong profit margins compared to **Consumer**.

---

## 9. Assumptions and Limitations

- Ambiguous dates (MM/DD vs DD/MM) defaulted to MM/DD/YYYY interpretation.
- Conflicting duplicate order_ids were flagged but not auto-resolved; manual review recommended.
- Original `sales` column preserved; `calculated_sales` added for verified values.
- No external validation of city/state/region mapping was performed.
- Screenshots show Python-rendered Excel output; native Excel views may differ slightly.

---

## 10. Screenshots Included

| File | Shows |
|------|-------|
| `screenshots/raw_data_preview.png` | First rows of raw dataset before cleaning |
| `screenshots/cleaned_data_preview.png` | Cleaned dataset with new calculated columns |
| `screenshots/pivot_summary_1.png` | Sales and Profit by Region pivot |
| `screenshots/pivot_summary_2.png` | Monthly Sales Trend pivot |

---

## Repository Structure

```
part1_data_cleaning/
├── data/
│   ├── raw_orders.xlsx
│   └── cleaned_orders.xlsx
├── outputs/
│   ├── data_quality_report.xlsx
│   ├── pivot_summary.xlsx
│   └── cleaning_log.md
├── screenshots/
│   ├── raw_data_preview.png
│   ├── cleaned_data_preview.png
│   ├── pivot_summary_1.png
│   └── pivot_summary_2.png
└── README.md
```
