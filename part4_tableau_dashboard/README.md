# Part 4: Tableau Executive Dashboard — Retail Sales Analysis

## 1. Business Problem Summary

The retail leadership team needed an executive dashboard to monitor and understand business performance across multiple dimensions: sales trends, regional performance, category profitability, customer segment behavior, shipping efficiency, discount impact, and return patterns. The objective was to build a Tableau dashboard that helps leadership identify actionable business opportunities and risks — not just a collection of charts, but a coherent data story supporting strategic decision-making.

---

## 2. Dataset Description

**File:** `data/dashboard_sales_data.xlsx`
**Sheet:** `dashboard_sales_data`
**Rows:** 4,200 orders
**Period:** January 2024 – December 2025

| Column | Type | Description |
|--------|------|-------------|
| order_id | String | Unique order identifier |
| order_date | Date | Date the order was placed |
| ship_date | Date | Date the order was shipped |
| customer_id | String | Unique customer identifier |
| customer_segment | String | Consumer, Corporate, or Home Office |
| region | String | North, South, East, West |
| state | String | Indian state name |
| city | String | City name |
| category | String | Furniture, Office Supplies, Technology |
| sub_category | String | Product sub-category (17 values) |
| product_name | String | Individual product name |
| ship_mode | String | Same Day, First Class, Second Class, Standard Class |
| sales | Float | Order revenue in ₹ |
| quantity | Integer | Number of units ordered |
| discount | Float | Discount applied (0.0 to 0.35) |
| profit | Float | Net profit in ₹ (can be negative) |
| return_flag | Integer | 1 = returned, 0 = not returned |
| delivery_days | Integer | Days between order and ship date |
| customer_rating | Float | Customer satisfaction rating (1–5) |
| campaign_channel | String | Organic, Social, Paid, Referral, Email (nullable) |

**Key Statistics:**
- Total Sales: ~₹217 million
- Total Profit: ~₹33.3 million
- Average Profit Margin: ~15.3%
- Overall Return Rate: ~4.55%
- Average Delivery Days: ~3.59

---

## 3. Tableau Workbook Description

**File:** `tableau/executive_dashboard.twbx`

The Tableau packaged workbook contains:
- 1 Executive Dashboard (main view)
- 7 supporting worksheet views
- 5 calculated fields
- 3 interactive filters with filter actions
- KPI summary cards at the top of the dashboard

The workbook uses the Excel dataset embedded directly (packaged workbook) and can be opened without any additional data connection configuration.

---

## 4. Calculated Fields Created

| Calculated Field | Formula Logic | Purpose |
|-----------------|---------------|---------|
| **Profit Margin** | `SUM([Profit]) / SUM([Sales])` | Measures profitability as a percentage of revenue |
| **Cost** | `[Sales] - [Profit]` | Derives cost of goods sold from sales and profit |
| **Average Order Value** | `SUM([Sales]) / COUNTD([Order ID])` | Measures average revenue per unique order |
| **Return Rate** | `SUM([Return Flag]) / COUNT([Order ID])` | Calculates percentage of orders returned |
| **Shipping Delay Bucket** | `IF [Delivery Days] <= 1 THEN "0–1 Days (Express)" ELSEIF [Delivery Days] <= 3 THEN "2–3 Days (Fast)" ELSEIF [Delivery Days] <= 5 THEN "4–5 Days (Standard)" ELSE "6+ Days (Delayed)" END` | Categorizes delivery speed into business-friendly buckets |

---

## 5. Dashboard Components

The executive dashboard includes the following components:

**KPI Cards (Top Row):**
- Total Sales
- Total Profit
- Overall Profit Margin %
- Return Rate %
- Average Order Value

**Charts/Views:**
1. Monthly Sales & Profit Trend (Line Chart)
2. Regional Performance Map (Filled Map)
3. Category Profitability (Horizontal Bar Chart)
4. Sub-Category Treemap (Treemap)
5. Customer Segment Comparison (Grouped Bar Chart)
6. Discount vs. Profit (Scatter Plot)
7. Shipping Performance (Bar Chart)
8. Return Rate Heatmap (Highlight Table)

---

## 6. Filters and Interactions Used

**Interactive Filters (available on dashboard):**
- Region (multi-select)
- Category (multi-select)
- Customer Segment (single-select)
- Order Date (date range slider)
- Ship Mode (multi-select)
- Campaign Channel (multi-select)

**Filter Actions:**
- Clicking a region on the map filters all other charts to that region
- Clicking a category bar highlights that category across all views
- Clicking a segment in the segment chart cross-filters the discount and return views

---

## 7. Key Business Insights

1. **Technology is the profit engine** — 18.22% margin vs. Furniture's 6.89%
2. **South region leads in revenue** (₹64.7M) but East has the best profit margin (15.55%)
3. **Discounts above 30% generate average losses** of ₹1,601 per order — a critical pricing risk
4. **Furniture has a 7.67% return rate** — more than double Technology's 3.03%
5. **Home Office is the most valuable segment** with the highest sales, profit, and margin
6. **Same Day shipping correlates with the highest average profit** (₹9,102/order)
7. **High discounts + Furniture + returns = compounding losses** (triple threat risk area)
8. **YoY sales grew 4.3%** from 2024 to 2025 with stable margins

See `outputs/business_insights.md` for the complete set of 10 business insights with data evidence and recommended actions.

---

## 8. Dashboard Story Summary

The dashboard tells a three-part story:

**Part 1 — The Winners:** Technology products, the South region, and the Home Office segment are the business's performance leaders. Same Day shipping commands premium profitability.

**Part 2 — The Risks:** Furniture's thin margins, high return rates, and the destructive impact of discounts above 20% represent the most urgent business risks. The Furniture–Discount–Return "triple threat" is generating compounding losses.

**Part 3 — The Opportunities:** The East and West regions are under-penetrated. A "Premium Technology" bundle offer could systematically drive more high-margin orders. Optimizing discount policy to a hard cap of 20% would immediately improve profitability.

See `outputs/dashboard_story.md` for the full leadership narrative.

---

## 9. Assumptions and Limitations

**Assumptions:**
- `profit` is assumed to reflect net margin after product cost and discount, but before operational overhead (shipping, returns handling, warehousing)
- `return_flag = 1` indicates a completed return; the cost of the return process is not quantified in the dataset
- `delivery_days` is calculated as the difference between `ship_date` and `order_date`; any pre-shipment processing delay is included
- `campaign_channel = null` orders are treated as unattributed/organic for analysis purposes

**Limitations:**
- No customer lifetime value can be calculated without individual customer purchase history linkage
- Return costs (reverse logistics, restocking) are not captured — true Furniture profitability may be worse than the 6.89% shown
- Campaign channel has null values for ~10–15% of orders, limiting marketing attribution analysis
- Two-year window (2024–2025) is insufficient to identify multi-year seasonal patterns with high confidence
- No competitor or market benchmark data available for context

---

## 10. Screenshots Included

| File | Content |
|------|---------|
| `screenshots/full_dashboard.png` | Complete executive dashboard with all charts and filters |
| `screenshots/sales_trend_view.png` | Monthly sales and profit trend line chart |
| `screenshots/regional_performance_view.png` | Regional map and bar chart |
| `screenshots/category_profitability_view.png` | Category and sub-category profitability view |
| `screenshots/filter_interaction_view.png` | Dashboard with a filter applied (e.g., Technology category selected) |

---

## Repository Structure

```
part4_tableau_dashboard/
├── data/
│   └── dashboard_sales_data.xlsx
├── tableau/
│   └── executive_dashboard.twbx
├── outputs/
│   ├── dashboard_story.md
│   ├── business_insights.md
│   └── chart_selection_justification.md
├── screenshots/
│   ├── full_dashboard.png
│   ├── sales_trend_view.png
│   ├── regional_performance_view.png
│   ├── category_profitability_view.png
│   └── filter_interaction_view.png
└── README.md
```
