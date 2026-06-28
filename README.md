# prabhatkumar_bitsom_ba_2511037_part3_regression_insights
# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary

A retail chain leadership team wants to understand what drives monthly sales performance across 80 stores. They are considering actions such as increasing marketing spend, improving inventory availability, changing discounting strategy, reallocating staff, and prioritising certain store types or regions. This analysis uses regression modelling to identify which factors are most strongly associated with monthly sales and provides an evidence-based business recommendation.

---

## Dataset Description

**File:** `data/business_regression_data.xlsx`
**Original records:** 320 (80 stores × 4 months: January–April 2025)
**Rows deleted:** 14 — 6 missing `competitor_distance_km`, 8 missing `customer_rating`
**Clean records used for all regression:** 306

| Column | Type | Role |
|---|---|---|
| store_id | Identifier | Not used in regression |
| month | Date | Not used (only 4 months — insufficient for time modelling) |
| region | Categorical | Converted to dummy variables (reference: East) |
| store_type | Categorical | Converted to dummy variables (reference: Residential) |
| marketing_spend | Numerical | Independent variable |
| footfall | Numerical | Independent variable |
| avg_discount_pct | Numerical | Independent variable |
| staff_count | Numerical | Independent variable |
| inventory_availability_pct | Numerical | Independent variable |
| competitor_distance_km | Numerical | Independent variable — **included in full model** |
| holiday_flag | Binary | Independent variable |
| customer_rating | Numerical | Independent variable — **included in full model** |
| monthly_sales | Numerical | **Dependent variable** |
| monthly_profit | Numerical | Outcome variable — not used as a predictor |

---

## Dependent and Independent Variables

**Dependent variable:** `monthly_sales`

**Independent variables in the multiple regression model (all 12 predictors):**
- 8 numerical: footfall, marketing_spend, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating
- 3 region dummies: region_North, region_South, region_West (reference = East)
- 3 store type dummies: store_Airport, store_High Street, store_Mall (reference = Residential)

---

## Regression Approach

1. **Simple Regression — Model 1:** footfall → monthly_sales (R² = 0.7348)
2. **Simple Regression — Model 2:** marketing_spend → monthly_sales (R² = 0.1574)
3. **Multiple Regression — Model 3:** all 12 predictors → monthly_sales (R² = 0.8550)
4. Models compared on R-squared, adjusted R-squared, variable significance, and business usefulness.
5. Predicted values and residuals computed from the final model for all 306 records.

---

## Dummy Variable Approach

**Region (reference = East):**
- region_North = 1 if North, 0 otherwise
- region_South = 1 if South, 0 otherwise
- region_West = 1 if West, 0 otherwise

**Store Type (reference = Residential):**
- store_Airport = 1 if Airport, 0 otherwise
- store_High Street = 1 if High Street, 0 otherwise
- store_Mall = 1 if Mall, 0 otherwise

One category is dropped from each group to avoid the dummy variable trap (perfect multicollinearity). The dropped category is the reference baseline. All coefficients measure the difference in expected sales compared to the reference category, holding all other variables constant.

---

## Model Comparison Summary

| Model | R-squared | Adj R-squared | Predictors | Recommended |
|---|---|---|---|---|
| Simple — Footfall | 0.7348 | — | 1 | No |
| Simple — Marketing Spend | 0.1574 | — | 1 | No |
| **Multiple Regression** | **0.8550** | **0.8480** | **14** | **✅ Yes** |

---

## Final Model Selected

**Multiple Regression — Full Model** (R² = 0.855, Adj R² = 0.848)

Explains 85.5% of monthly sales variation using all 12 predictors. 13 of 14 variables are statistically significant (p < 0.05). Only average discount percentage is not significant (p = 0.373). The improvement over simple regression is genuine — adjusted R² confirms that the additional variables contribute real explanatory value.

---

## Business Recommendation

1. **Footfall is the primary lever.** Drive more customers into stores through loyalty programmes, local events, click-and-collect, and improved accessibility.
2. **Improve inventory availability.** Each 1 percentage point improvement adds ~£2,786 in monthly sales. Reduce stockouts and improve replenishment speed.
3. **Customer experience matters.** Each 1-point improvement in customer rating is associated with ~£12,750 more in monthly sales. Invest in staff training and complaints resolution.
4. **Airport and Mall formats outperform.** Factor structural premiums (£30K–£43K/month) into site selection and capital allocation decisions.
5. **Marketing spend returns are modest.** £1.23 per £1 spent. Focus on efficiency and footfall impact, not raw budget size.
6. **Do not over-rely on discounting.** Average discount % is not statistically significant in the full model.

---

## Assumptions and Limitations

- Short observation window: 4 months only. Seasonal trading patterns not fully captured.
- Multicollinearity: footfall, staff count, and store size are related. Individual coefficients are directional guides, not independent effects.
- Missing variables: local demographics, online channel performance, and competitor quality not included.
- Regression shows association, not causation. Controlled experiments are needed before committing to major investment changes based on model results alone.
- 14 records with missing values were deleted before analysis.
