# Residual Analysis

## Final Model Used
**Multiple Regression (MR – Full Model)**  
Dependent Variable: `monthly_sales`  
R² = 0.8312

---

## How Residuals Were Calculated

- **Predicted Sales** = Model output using all 10 predictors for each store-month record
- **Residual** = Actual Monthly Sales − Predicted Monthly Sales
- A **positive residual** means the store performed *better* than the model predicted
- A **negative residual** means the store performed *worse* than the model predicted

---

## Top 5 Records with Largest Positive Residuals

| Store ID | Region | Store Type | Actual Sales ($) | Predicted Sales ($) | Residual ($) |
|---|---|---|---|---|---|
| STR-1028 | East | Mall | 713,611.16 | 597,728.90 | +115,882.26 |
| STR-1073 | East | Residential | 813,316.71 | 702,191.72 | +111,124.99 |
| STR-1019 | East | Residential | 788,087.68 | 697,763.25 | +90,324.43 |
| STR-1026 | East | Mall | 625,514.04 | 538,360.63 | +87,153.41 |
| STR-1050 | North | Residential | 735,786.64 | 648,707.87 | +87,078.77 |

---

## Top 5 Records with Largest Negative Residuals

| Store ID | Region | Store Type | Actual Sales ($) | Predicted Sales ($) | Residual ($) |
|---|---|---|---|---|---|
| STR-1017 | West | High Street | 685,379.08 | 844,584.67 | -159,205.59 |
| STR-1023 | South | Mall | 627,171.90 | 769,876.32 | -142,704.42 |
| STR-1012 | West | Residential | 595,467.60 | 713,036.41 | -117,568.81 |
| STR-1007 | West | Mall | 800,451.94 | 915,003.99 | -114,552.05 |
| STR-1009 | North | Residential | 641,865.03 | 743,049.09 | -101,184.06 |

---

## Business Interpretation of Residuals

### Large Positive Residuals (Model Under-predicts)
Stores like **STR-1028** (East/Mall) and **STR-1073** (East/Residential) sold significantly more than the model expected. This could mean:
- These stores have **exceptional store managers or sales teams** not captured in the data
- They may have run **exclusive promotions or local events** that drove unusual traffic
- **Brand loyalty or local reputation** may be higher than average for the region/type

These stores are **outperformers** — leadership should study them to understand what they're doing differently and replicate those practices.

### Large Negative Residuals (Model Over-predicts)
Stores like **STR-1017** (West/High Street) and **STR-1023** (South/Mall) sold far less than predicted. Possible reasons:
- **Local competitive pressure** (nearby competitors) not captured in the model
- **Operational issues** such as stockouts, staffing problems, or poor service
- **Location-specific factors** such as construction, access difficulties, or neighborhood decline
- STR-1017 and STR-1007 are both **West region** — this may indicate a regional issue the model's West dummy doesn't fully capture

These stores are **underperformers** — they warrant urgent investigation by regional managers.

---

## Is the Model Under- or Over-predicting Certain Store Types?

- **West region stores** appear more frequently in large negative residuals (STR-1017, STR-1012, STR-1007) — the model may be **over-predicting** West region performance despite including a West dummy variable. There may be localized factors (competition, demographics) not fully captured.
- **East Residential stores** appear in large positive residuals — the model may be **under-predicting** for top East performers, suggesting exceptional store-level factors.
- **No systematic bias** is apparent across all store types overall, which is expected for a well-fitted OLS model (residuals should sum to approximately zero).

---

## Summary

The residual analysis suggests the model performs well overall (R² = 0.83) but misses store-specific and hyper-local factors. The largest errors occur in West-region stores (over-predicted) and select East-region stores (under-predicted), pointing to unmeasured local dynamics that leadership should investigate directly.
