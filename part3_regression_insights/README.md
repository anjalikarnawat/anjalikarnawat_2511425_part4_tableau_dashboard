# Part 3: Regression-Based Business Insights & Model Interpretation

## 1. Business Problem Summary

A retail chain leadership team wants to understand which factors are most strongly associated with monthly store sales (`monthly_sales`). They are considering business actions such as increasing marketing spend, improving inventory availability, changing discounting strategy, reallocating staff, and prioritizing certain store types or regions. Regression analysis is used to identify the strongest predictors and provide evidence-based business recommendations.

---

## 2. Dataset Description

**File:** `data/business_regression_data.xlsx`  
**Rows:** 320 observations (80 stores × 4 months: Jan–Apr 2025)  
**Columns:** 14 variables

| Column | Type | Description |
|---|---|---|
| store_id | Categorical (ID) | Unique store identifier |
| month | Date | Month of record |
| region | Categorical | Store region: East, North, South, West |
| store_type | Categorical | Store type: Residential, High Street, Airport, Mall |
| marketing_spend | Numerical | Monthly marketing expenditure ($) |
| footfall | Numerical | Number of customer visits |
| avg_discount_pct | Numerical | Average discount given (%) |
| staff_count | Numerical | Number of staff members |
| inventory_availability_pct | Numerical | % of items available in stock |
| competitor_distance_km | Numerical | Distance to nearest competitor (km) |
| holiday_flag | Binary (0/1) | Whether month includes a major holiday |
| customer_rating | Numerical | Average customer satisfaction rating |
| monthly_sales | Numerical | **Target / Dependent Variable** ($) |
| monthly_profit | Numerical | Monthly profit (not used as predictor) |

**Missing Values:**
- `competitor_distance_km`: 6 missing → filled with median (27.37 km)
- `customer_rating`: 8 missing → filled with median

---

## 3. Dependent and Independent Variables

**Dependent Variable:** `monthly_sales`

**Independent Variables used in regression:**
- Numerical: `marketing_spend`, `footfall`, `inventory_availability_pct`, `customer_rating`
- Dummy (from Categorical): `region_North`, `region_South`, `region_West`, `store_HighStreet`, `store_Airport`, `store_Mall`

**Variables NOT used / limited usefulness:**
- `store_id`: Identifier only
- `month`: Temporal variable, not a direct predictor
- `avg_discount_pct`: Not statistically significant (p=0.10)
- `staff_count`: Correlated with footfall; dropped to avoid multicollinearity
- `competitor_distance_km`: Weak predictor; excluded from final model
- `holiday_flag`: Binary; marginal contribution when footfall is included
- `monthly_profit`: Outcome variable, not a predictor

---

## 4. Regression Approach

Three regression models were built:
1. **SR1 – Simple Regression (Footfall):** `monthly_sales ~ footfall`
2. **SR2 – Simple Regression (Marketing Spend):** `monthly_sales ~ marketing_spend`
3. **MR – Multiple Regression (Full Model):** All key numerical + dummy variables

All models use Ordinary Least Squares (OLS). Models were evaluated using R², Adjusted R², and p-values.

---

## 5. Dummy Variable Approach

**Region** (4 categories → 3 dummies, reference = **East**):
- `region_North` = 1 if North, else 0
- `region_South` = 1 if South, else 0
- `region_West` = 1 if West, else 0

**Store Type** (4 categories → 3 dummies, reference = **Residential**):
- `store_HighStreet` = 1 if High Street, else 0
- `store_Airport` = 1 if Airport, else 0
- `store_Mall` = 1 if Mall, else 0

The reference categories (East and Residential) are excluded to avoid the **dummy variable trap** (perfect multicollinearity). All coefficients are interpreted relative to the reference category.

---

## 6. Model Comparison Summary

| Model | Variables | R² | Key Significant Variables |
|---|---|---|---|
| SR1 – Footfall | footfall | 0.7363 | footfall |
| SR2 – Marketing Spend | marketing_spend | 0.1672 | marketing_spend |
| MR – Full Model | 10 predictors | 0.8312 | footfall, marketing_spend, inventory_availability_pct, customer_rating, region_South, region_West, store_HighStreet, store_Airport, store_Mall |

---

## 7. Final Model Selected

**Multiple Regression (MR – Full Model)**

R² = 0.8312 — the model explains **83.1%** of the variation in monthly sales, outperforming both simple regression models. It incorporates both numerical and categorical variables, providing richer and more actionable business insights.

---

## 8. Business Recommendation

**Priority actions for the retail chain:**
1. **Drive footfall** — the single strongest predictor (R² = 0.74 alone). Invest in in-store events, loyalty programs, and location marketing.
2. **Increase marketing spend** — each additional $1 in marketing is associated with ~$1.21 more in sales.
3. **Improve inventory availability** — each 1% gain in availability → ~$3,048 additional monthly sales.
4. **Improve customer ratings** — a 1-point improvement in rating is linked to ~$13,521 more in monthly sales.
5. **Prioritize Airport and Mall stores** — these outperform Residential stores by ~$42,662 and ~$29,375 respectively.

---

## 9. Assumptions and Limitations

- Regression shows **association, not causation**. A store with high footfall may also have better location, management, or brand — these confounding factors are not captured.
- The model assumes **linear relationships** between predictors and sales.
- `region_North` was **not statistically significant** (p=0.39) and should not be used for decisions.
- The dataset covers only **4 months**, limiting seasonal generalizability.
- Missing values were **imputed with medians**, which may introduce slight bias.
- External factors (weather, macroeconomic shifts, competitor promotions) are **not included**.

---

## 10. Screenshots Included

| File | Contents |
|---|---|
| `screenshots/simple_regression_output.png` | SR1 Footfall regression output |
| `screenshots/multiple_regression_output.png` | Multiple regression output |
| `screenshots/residuals_preview.png` | Predictions and residuals table |
| `screenshots/model_comparison_preview.png` | Model comparison table |

---

## Repository Structure

```
part3_regression_insights/
├── data/
│   └── business_regression_data.xlsx
├── analysis/
│   ├── regression_workbook.xlsx
│   ├── model_comparison.md
│   └── residual_analysis.md
├── outputs/
│   ├── regression_summary.xlsx
│   ├── final_recommendation.md
│   └── model_equations.md
├── screenshots/
│   ├── simple_regression_output.png
│   ├── multiple_regression_output.png
│   ├── residuals_preview.png
│   └── model_comparison_preview.png
└── README.md
```
