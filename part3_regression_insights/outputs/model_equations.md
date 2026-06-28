# Model Equations

---

## Simple Regression Equations

### SR1 – Monthly Sales ~ Footfall

```
monthly_sales = 446,410.58 + 35.68 × footfall
```

| Term | Value | Explanation |
|---|---|---|
| Intercept | 446,410.58 | Estimated baseline sales when footfall = 0 (theoretical floor) |
| footfall coefficient | 35.68 | Each additional visitor is associated with ~$35.68 more in monthly sales |
| R-Squared | 0.7363 | Footfall alone explains 73.6% of sales variation |
| P-Value (footfall) | < 0.0001 | Highly statistically significant |

**Business meaning:** Footfall is the strongest single driver of sales. Stores with higher customer traffic consistently achieve much higher revenues.

---

### SR2 – Monthly Sales ~ Marketing Spend

```
monthly_sales = 560,777.35 + 2.13 × marketing_spend
```

| Term | Value | Explanation |
|---|---|---|
| Intercept | 560,777.35 | Estimated baseline sales when marketing spend = 0 |
| marketing_spend coefficient | 2.13 | Each additional $1 in marketing is associated with ~$2.13 more in monthly sales |
| R-Squared | 0.1672 | Marketing spend alone explains 16.7% of sales variation |
| P-Value (marketing_spend) | < 0.0001 | Statistically significant, but weaker predictor alone |

**Business meaning:** Marketing investment has a measurable positive return (~2× ROI in sales), but many other factors also influence sales.

---

## Multiple Regression Equation

### MR – Full Multiple Regression Model

```
monthly_sales = 39,522.73
              + 1.21 × marketing_spend
              + 34.01 × footfall
              + 3,048.11 × inventory_availability_pct
              + 13,520.58 × customer_rating
              + 6,089.50 × region_North
              + 20,117.94 × region_South
              + 18,492.64 × region_West
              + 18,102.54 × store_HighStreet
              + 42,662.45 × store_Airport
              + 29,375.42 × store_Mall
```

**R-Squared: 0.8312 | Adjusted R-Squared: 0.8257**

---

## Coefficient Explanations

| Variable | Coefficient | P-Value | Significant? | Business Interpretation |
|---|---|---|---|---|
| Intercept | 39,522.73 | 0.40 | No | Theoretical baseline; not meaningful on its own |
| marketing_spend | 1.21 | < 0.0001 | **Yes** | Every $1 extra in marketing → ~$1.21 more in sales (holding all else constant) |
| footfall | 34.01 | < 0.0001 | **Yes** | Each additional visitor → ~$34.01 more in sales |
| inventory_availability_pct | 3,048.11 | < 0.0001 | **Yes** | Each 1% gain in stock availability → ~$3,048 more in sales |
| customer_rating | 13,520.58 | 0.005 | **Yes** | A 1-point rating improvement → ~$13,521 more in sales |
| region_North | 6,089.50 | 0.387 | **No** | North stores not significantly different from East stores |
| region_South | 20,117.94 | 0.005 | **Yes** | South stores earn ~$20,118 more than East stores (reference) |
| region_West | 18,492.64 | 0.003 | **Yes** | West stores earn ~$18,493 more than East stores (reference) |
| store_HighStreet | 18,102.54 | 0.003 | **Yes** | High Street stores earn ~$18,103 more than Residential (reference) |
| store_Airport | 42,662.45 | < 0.0001 | **Yes** | Airport stores earn ~$42,662 more than Residential stores |
| store_Mall | 29,375.42 | < 0.0001 | **Yes** | Mall stores earn ~$29,375 more than Residential stores |

---

## Dummy Variable Explanation

Categorical variables cannot be used directly in regression. They must be converted to **dummy (binary) variables** — one for each category except one (the **reference category**), to avoid perfect multicollinearity (the "dummy variable trap").

### Region Dummies
- **Reference Category: East** (excluded from model)
- Created: `region_North`, `region_South`, `region_West`
- Interpretation: coefficients show how much each region's sales differ *from East stores*, holding all other variables constant

### Store Type Dummies
- **Reference Category: Residential** (excluded from model)
- Created: `store_HighStreet`, `store_Airport`, `store_Mall`
- Interpretation: coefficients show how much each store type's sales differ *from Residential stores*, all else equal

---

## Final Model Selected

**MR – Multiple Regression (Full Model)**

### Reason for Selection:
1. **Highest R²** (0.8312) — explains 83.1% of sales variation vs 73.6% and 16.7% for simple models
2. **Incorporates both numerical and categorical predictors** — gives richer, multi-dimensional business insights
3. **9 out of 10 predictors are statistically significant** — reliable, actionable coefficients
4. **Adjusted R² remains high** (0.8257) — the improvement is genuine, not just from adding more variables
5. **Business relevance** — covers marketing, operations, customer experience, and store/regional characteristics

The multiple regression model provides leadership with a comprehensive tool to understand and predict monthly sales across their store network.
