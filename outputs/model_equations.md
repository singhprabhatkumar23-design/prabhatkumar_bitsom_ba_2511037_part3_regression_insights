# Model Equations

## Simple Regression Models

### Model 1: Footfall → Monthly Sales

**Equation:**
`Monthly Sales = 447,699.03 + 35.64 × Footfall`

| Parameter | Value |
|---|---|
| Intercept | 447,699.03 |
| Coefficient (Footfall) | 35.64 |
| R-squared | 0.7348 |
| P-value | < 0.001 |

**Business meaning:** Every additional customer walking into a store generates approximately £35.64 in sales. For every 1,000 extra visitors a month, the model expects roughly £35,640 more in revenue. Footfall alone explains 73.5% of the variation in monthly sales — making it the strongest single predictor in the entire dataset.

---

### Model 2: Marketing Spend → Monthly Sales

**Equation:**
`Monthly Sales = 567,463.56 + 2.05 × Marketing Spend`

| Parameter | Value |
|---|---|
| Intercept | 567,463.56 |
| Coefficient (Marketing Spend) | 2.05 |
| R-squared | 0.1574 |
| P-value | < 0.001 |

**Business meaning:** Each additional £1 spent on marketing is associated with approximately £2.05 more in monthly sales. While statistically significant, marketing spend on its own explains only 15.7% of sales variation — a considerably weaker predictor than footfall. Some stores with very high marketing spend did not see proportionally higher sales, suggesting diminishing returns at large spend levels.

---

## Multiple Regression Model

### Full Model: All 12 Predictors (8 Numerical + 4 Dummy Variables)

**Clean dataset used:** 306 records (14 rows deleted — had missing values in `competitor_distance_km` or `customer_rating`)

**Equation:**
```
Monthly Sales = 60,960
  + 27.11 × Footfall
  + 1.23 × Marketing Spend
  – 30,940 × Avg Discount %
  + 3,721.22 × Staff Count
  + 2,785.92 × Inventory Availability %
  – 3,524.84 × Competitor Distance (km)
  + 14,040 × Holiday Flag
  + 12,750 × Customer Rating
  + 13,670 × Region_North
  + 24,920 × Region_South
  + 28,390 × Region_West
  + 42,600 × Store_Airport
  + 18,640 × Store_High Street
  + 30,740 × Store_Mall
```

| Variable | Coefficient | P-value | Significant? |
|---|---|---|---|
| Intercept | 60,960 | 0.190 | — |
| Footfall | 27.11 | < 0.001 | ✅ Yes |
| Marketing Spend | 1.23 | < 0.001 | ✅ Yes |
| Avg Discount % | –30,940 | 0.373 | ❌ No |
| Staff Count | 3,721.22 | 0.002 | ✅ Yes |
| Inventory Availability % | 2,785.92 | < 0.001 | ✅ Yes |
| Competitor Distance (km) | –3,524.84 | < 0.001 | ✅ Yes |
| Holiday Flag | 14,040 | 0.023 | ✅ Yes |
| Customer Rating | 12,750 | 0.005 | ✅ Yes |
| Region: North | 13,670 | 0.044 | ✅ Yes |
| Region: South | 24,920 | < 0.001 | ✅ Yes |
| Region: West | 28,390 | < 0.001 | ✅ Yes |
| Store: Airport | 42,600 | < 0.001 | ✅ Yes |
| Store: High Street | 18,640 | 0.001 | ✅ Yes |
| Store: Mall | 30,740 | < 0.001 | ✅ Yes |

**R-squared: 0.8550 | Adjusted R-squared: 0.8480 | F-statistic: 123.0 (p < 0.001)**

---

## What Each Coefficient Means in Business Terms

| Variable | Business Meaning |
|---|---|
| **Footfall (+27.11)** | Each extra customer visit per month generates ~£27 in sales. Still the strongest operational lever. |
| **Marketing Spend (+1.23)** | Each extra £1 of marketing spend generates ~£1.23 in sales. Positive return but modest — efficiency matters. |
| **Avg Discount % (–30,940)** | Higher discounting is weakly associated with lower sales in this model, but the effect is not statistically significant once all other factors are controlled. Do not over-interpret. |
| **Staff Count (+3,721)** | Each additional staff member is associated with ~£3,721 more in monthly sales. Likely reflects better service and store capacity. |
| **Inventory Availability % (+2,786)** | Each 1 percentage point improvement in inventory availability adds ~£2,786 in monthly sales. Stocking shelves consistently pays off. |
| **Competitor Distance (–3,525)** | Each extra kilometre from the nearest competitor is associated with ~£3,525 less in monthly sales. Stores in competitive areas tend to perform better — likely because they are located in busier, more accessible locations. |
| **Holiday Flag (+14,040)** | Months containing a public holiday generate ~£14,040 more in sales on average. |
| **Customer Rating (+12,750)** | Each 1-point increase in customer rating is associated with ~£12,750 more in monthly sales. Customer experience matters. |
| **Region North (+13,670)** | North region stores generate ~£13,670 more per month than East stores, all else equal. |
| **Region South (+24,920)** | South region stores generate ~£24,920 more per month than East stores. |
| **Region West (+28,390)** | West region stores generate ~£28,390 more per month than East stores — the strongest regional premium. |
| **Store Airport (+42,600)** | Airport stores generate ~£42,600 more per month than Residential stores — the highest store-type premium. |
| **Store Mall (+30,740)** | Mall stores generate ~£30,740 more per month than Residential stores. |
| **Store High Street (+18,640)** | High Street stores generate ~£18,640 more per month than Residential stores. |

---

## Dummy Variable Approach

### Why Dummy Variables?

Region and store type are categorical — the model cannot use text labels like "East" or "Airport" in a regression equation. Dummy variables convert these into binary (0/1) columns the model can work with.

### Region Dummies (Reference Category: **East**)

| Dummy Column | Value = 1 | Value = 0 |
|---|---|---|
| region_North | Store is in North | Store is not in North |
| region_South | Store is in South | Store is not in South |
| region_West | Store is in West | Store is not in West |

East region is the reference. All region coefficients represent the expected sales difference compared to an East region store with identical characteristics.

### Store Type Dummies (Reference Category: **Residential**)

| Dummy Column | Value = 1 | Value = 0 |
|---|---|---|
| store_Airport | Airport store | Not an Airport store |
| store_High Street | High Street store | Not a High Street store |
| store_Mall | Mall store | Not a Mall store |

Residential store type is the reference. All store type coefficients represent the expected sales premium above a Residential store of otherwise identical characteristics.

### Why is One Category Dropped?

If all 4 region categories were included (East, North, South, West), their dummy columns would always sum to 1 — meaning one column is perfectly predictable from the others. This creates perfect multicollinearity and makes the model unsolvable. Dropping one (the reference category) resolves this. The dropped category is not ignored — it is the baseline everything else is measured against.

---

## Final Model Selected

**Selected Model:** Multiple Regression — Full Model (14 predictors, R² = 0.855)

**Reason for selection:** The full multiple regression model explains 85.5% of the variation in monthly sales, compared to 73.5% for the best simple regression model (footfall alone). The adjusted R² of 0.848 confirms all additional variables genuinely contribute — the improvement is not just from adding more variables. The model is statistically significant as a whole (F-statistic p < 0.001), and 13 out of 14 predictors are individually significant at the 5% level. Only average discount percentage fails to reach significance. This model gives leadership the most complete, evidence-based picture of what drives store sales performance.
