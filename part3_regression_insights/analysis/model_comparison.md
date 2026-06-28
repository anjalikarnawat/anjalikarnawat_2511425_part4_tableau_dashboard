# Model Comparison

## Overview

Three regression models were built and compared to predict `monthly_sales` for a retail chain dataset of 320 observations (80 stores, 4 months).

---

## Model 1: SR1 – Simple Regression (Footfall)

| Item | Detail |
|---|---|
| **Model Name** | SR1 – Footfall Simple Regression |
| **Dependent Variable** | monthly_sales |
| **Independent Variable** | footfall |
| **R-Squared** | 0.7363 |
| **Significant Variables** | footfall (p < 0.0001) |
| **Equation** | monthly_sales = 446,410.58 + 35.68 × footfall |
| **Business Usefulness** | Strong model for understanding foot traffic's impact on revenue. Useful for store opening hours, location decisions, and event planning. |
| **Limitations** | Ignores marketing spend, inventory, customer satisfaction, store type, and region — all of which matter. |

---

## Model 2: SR2 – Simple Regression (Marketing Spend)

| Item | Detail |
|---|---|
| **Model Name** | SR2 – Marketing Spend Simple Regression |
| **Dependent Variable** | monthly_sales |
| **Independent Variable** | marketing_spend |
| **R-Squared** | 0.1672 |
| **Significant Variables** | marketing_spend (p < 0.0001) |
| **Equation** | monthly_sales = 560,777.35 + 2.13 × marketing_spend |
| **Business Usefulness** | Provides an estimated ROI on marketing: each $1 spent is associated with ~$2.13 in additional sales. Useful for budget planning. |
| **Limitations** | Explains only ~16.7% of sales variation. Marketing alone is a weak predictor. Other factors drive the majority of sales differences. |

---

## Model 3: MR – Multiple Regression (Full Model)

| Item | Detail |
|---|---|
| **Model Name** | MR – Multiple Regression (Full Model) |
| **Dependent Variable** | monthly_sales |
| **Independent Variables** | marketing_spend, footfall, inventory_availability_pct, customer_rating, region_North, region_South, region_West, store_HighStreet, store_Airport, store_Mall |
| **R-Squared** | 0.8312 |
| **Adj. R-Squared** | 0.8257 |
| **Significant Variables** | footfall, marketing_spend, inventory_availability_pct, customer_rating, region_South, region_West, store_HighStreet, store_Airport, store_Mall |
| **Non-Significant** | const (intercept, p=0.40), region_North (p=0.39) |
| **Business Usefulness** | Best model. Explains 83.1% of sales variance. Captures multi-dimensional drivers including operations, marketing, customer experience, and store/region characteristics. Actionable for leadership. |
| **Limitations** | Does not capture seasonal trends (only 4 months), competitor behavior, staff quality, or macroeconomic factors. region_North is not significant and should not drive regional resource decisions. |

---

## Side-by-Side Comparison

| Metric | SR1 (Footfall) | SR2 (Marketing) | MR (Full) |
|---|---|---|---|
| R-Squared | 0.7363 | 0.1672 | **0.8312** |
| Adj. R-Squared | N/A | N/A | **0.8257** |
| # Predictors | 1 | 1 | 10 |
| Significant Vars | 1 | 1 | 9 |
| Captures Store Type? | No | No | **Yes** |
| Captures Region? | No | No | **Yes** |
| Best for Decision Making? | Partial | Partial | **Yes** |

---

## Conclusion

The **Multiple Regression (MR) model is recommended** as the final model. It substantially outperforms both simple regression models in explanatory power (R² = 0.83 vs 0.74 and 0.17) while providing a multi-factor view of what drives sales — essential for leadership-level decision-making across marketing, operations, and store strategy.
