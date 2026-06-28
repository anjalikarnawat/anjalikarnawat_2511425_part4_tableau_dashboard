# Chart Selection Justification
**Dashboard:** Executive Sales Dashboard — Retail Leadership Team
**Tool:** Tableau Desktop

---

## Chart 1: Sales Trend View — Line Chart (Monthly/Quarterly Sales Over Time)

**Business Question Answered:**
How are total sales and profit trending over time? Are we growing, flat, or declining?

**Why This Chart Type Is Appropriate:**
A line chart is the standard and most intuitive tool for visualizing continuous change over time. It allows the viewer to immediately identify growth trends, seasonal patterns, dips, and inflection points. For a leadership audience reviewing a time series of sales over 2 years, a line chart communicates direction, pace, and volatility in a single glance.

**Fields Used:**
- X-axis: Order Date (continuous, aggregated to Month or Quarter)
- Y-axis: SUM(Sales) and SUM(Profit) — dual axis
- Color: Measure Names (to distinguish Sales vs. Profit lines)
- Tooltip: Month, Total Sales, Total Profit, Profit Margin %

**Design Principle Applied:**
Dual-axis line chart allows simultaneous viewing of sales and profit trends without doubling the chart count. Colors are kept to two (blue for Sales, green for Profit) to avoid confusion. Y-axis starts at 0 to avoid misleading scale distortion. Chart title is clear: "Monthly Sales & Profit Trend (2024–2025)."

**Mistake Avoided:**
Avoided using a bar chart for this time series, as bars emphasize individual values and obscure trend direction. Avoided using more than two measures on the same axis, which creates clutter. Did not truncate the Y-axis to exaggerate growth.

---

## Chart 2: Regional Performance View — Filled Map + Bar Chart

**Business Question Answered:**
Which regions are generating the most revenue and profit? Are there geographic imbalances?

**Why This Chart Type Is Appropriate:**
A filled map (choropleth) immediately communicates geographic concentration and regional imbalance. Leadership can see at a glance which states/regions are performing well (darker color) and which are underperforming (lighter color). A companion bar chart provides the exact numbers for comparison. For a retail business operating across Indian regions (North, South, East, West), geography is a natural dimension to visualize.

**Fields Used:**
- Map: State (geographic field) → Color = SUM(Profit) or SUM(Sales)
- Bar Chart: Region → X-axis (Sales), Y-axis sorted descending
- Color: Profit Margin % (diverging palette — red for low, blue-green for high)
- Size (bubble variant): SUM(Sales)
- Tooltip: Region, State, Total Sales, Total Profit, Profit Margin %

**Design Principle Applied:**
Single sequential color palette on the map — from light to dark — to indicate increasing performance. Regions labeled directly on bars. Bars sorted in descending order so the viewer immediately sees the ranking. No 3D effects or unnecessary decoration.

**Mistake Avoided:**
Avoided using a pie chart for regional sales share, as pie charts are poor at communicating ranked comparisons across more than 2–3 segments. Avoided using multiple conflicting color schemes between the map and bar chart (kept them consistent).

---

## Chart 3: Category Profitability View — Horizontal Bar Chart + Treemap

**Business Question Answered:**
Which categories and sub-categories drive the most profit? Which are underperforming?

**Why This Chart Type Is Appropriate:**
A horizontal bar chart is ideal for comparing profit across a moderate number of categories (3 categories, ~17 sub-categories). Horizontal orientation allows long sub-category names to be fully readable without rotation. A treemap adds a second dimension — both profit magnitude (area) and margin (color) — giving leadership an intuitive sense of both size and efficiency simultaneously.

**Fields Used:**
- Bar Chart: Sub-Category → X-axis (SUM Profit), sorted descending; Category as color
- Treemap: Category/Sub-Category → Size = SUM(Sales), Color = Profit Margin %
- Color Palette: Diverging (red = low/negative margin, green = high margin)
- Tooltip: Category, Sub-Category, Sales, Profit, Profit Margin %

**Design Principle Applied:**
Diverging color palette on the treemap immediately highlights which sub-categories are "in the red" vs. performing well. Reference line added to bar chart at the average profit margin to provide context. Consistent category color coding (e.g., Technology = blue, Furniture = orange, Office Supplies = green) maintained across all views.

**Mistake Avoided:**
Avoided using a stacked bar chart for sub-category comparison, as stacked bars make it difficult to compare non-baseline segments. Avoided using a 3D pie chart, which is one of the most misleading chart types for categorical comparisons.

---

## Chart 4: Customer Segment View — Grouped Bar Chart

**Business Question Answered:**
How do the three customer segments (Consumer, Corporate, Home Office) compare on sales, profit, and return rate?

**Why This Chart Type Is Appropriate:**
A grouped (clustered) bar chart allows direct side-by-side comparison of multiple measures across a small number of categories. With only 3 segments and 2–3 measures to compare, a grouped bar chart gives clear visual differentiation without clutter.

**Fields Used:**
- X-axis: Customer Segment (Consumer, Corporate, Home Office)
- Y-axis: SUM(Sales) — primary bars
- Secondary measure: Profit Margin % — line overlay or color label
- Color: Segment (consistent across all views)
- Tooltip: Segment, Sales, Profit, Profit Margin %, Order Count, Return Rate %

**Design Principle Applied:**
Consistent segment colors are used across every view so leadership can quickly cross-reference a segment across different charts. Bars are labeled with values to avoid guessing from the axis. Sort order kept consistent (alphabetical or by value) so the eye doesn't need to re-orient between charts.

**Mistake Avoided:**
Avoided using a radar/spider chart for multi-measure comparison, as radar charts are difficult for non-technical audiences to interpret accurately. Did not use pie charts for segment share comparison.

---

## Chart 5: Shipping Performance View — Bar Chart (Ship Mode vs. Avg Delivery Days + Profit)

**Business Question Answered:**
Which shipping mode delivers orders fastest, and does faster shipping correlate with higher profit?

**Why This Chart Type Is Appropriate:**
A bar chart comparing ship modes on average delivery days is the clearest choice — it allows instant ranking comparison. Adding a secondary axis or color encoding for average profit adds the business dimension without adding chart complexity.

**Fields Used:**
- X-axis: Ship Mode (Same Day, First Class, Second Class, Standard Class)
- Y-axis (primary): AVG(Delivery Days) — bar height
- Y-axis (secondary) or Color: AVG(Profit) — line or label overlay
- Tooltip: Ship Mode, Avg Delivery Days, Avg Profit, Total Orders, Return Rate %

**Design Principle Applied:**
Bars sorted in ascending order of delivery days (Same Day → Standard Class) to create a natural visual narrative of speed vs. profitability. Reference line added at the overall average delivery days for context. Color used to distinguish the profit dimension without adding unnecessary chart elements.

**Mistake Avoided:**
Avoided using a scatter plot for this view (scatter plots require more than 4 data points to be meaningful). Avoided using a stacked bar that would obscure the comparison of individual metrics.

---

## Chart 6: Discount vs. Profit View — Scatter Plot

**Business Question Answered:**
What is the relationship between discount rate and order profitability? Does discounting help or hurt the business?

**Why This Chart Type Is Appropriate:**
A scatter plot is the ideal chart for revealing correlation between two continuous numerical variables. With discount (%) on the X-axis and profit (₹) on the Y-axis, each point represents one order, and the overall scatter pattern instantly communicates the direction and strength of the relationship. A trend line can be overlaid to quantify the relationship.

**Fields Used:**
- X-axis: Discount (continuous)
- Y-axis: Profit (continuous)
- Color: Category (to reveal if the discount-profit relationship differs by category)
- Size: Sales (to show which orders are larger)
- Tooltip: Order ID, Discount %, Profit, Category, Segment
- Analytics: Trend line (linear or polynomial)

**Design Principle Applied:**
Transparency (opacity ~50–70%) applied to individual marks to reveal density in overlapping areas. A reference line at Profit = 0 added to visually separate profitable orders (above the line) from loss-making orders (below the line). Trend line clearly labeled with slope direction and R² value.

**Mistake Avoided:**
Avoided using a line chart for this view, as a line chart implies a time sequence which is not the intended story here. Avoided binning discount into categories and using a bar chart, which would obscure individual-order variation. Avoided removing the zero-profit reference line, which is critical for understanding the loss threshold.

---

## Chart 7: Return Analysis View — Bar Chart / Highlight Table

**Business Question Answered:**
Which categories, sub-categories, and customer segments have the highest return rates? Where is return risk concentrated?

**Why This Chart Type Is Appropriate:**
A highlight table (heat map) is ideal for showing return rates across two dimensions simultaneously (e.g., Category × Segment). Color intensity immediately draws the eye to high-return combinations. A companion bar chart shows total return volume by category.

**Fields Used:**
- Rows: Customer Segment
- Columns: Category
- Color: Return Rate % — sequential color (light = low risk, dark red = high risk)
- Size (bar variant): Count of Returned Orders
- Tooltip: Category, Segment, Total Orders, Returned Orders, Return Rate %

**Design Principle Applied:**
A diverging red color palette is used for the highlight table — white at the average return rate, red for above-average, to instantly flag risk areas. Values displayed inside cells for readability. Chart title specifically states "Return Rate by Category and Segment" to eliminate ambiguity.

**Mistake Avoided:**
Avoided using a line chart for return rates, as return rate is a categorical metric, not a time series (in this view). Avoided using a 3D bar chart which would distort the visual comparison. Did not use more than two dimensions in the same chart to prevent confusion.
