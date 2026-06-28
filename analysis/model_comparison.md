# Model Comparison

**Dataset used for all models:** Clean file — 306 records (14 rows deleted due to missing values in `competitor_distance_km` or `customer_rating`)

---

## Comparison Table

| Item | Model 1: Simple – Footfall | Model 2: Simple – Marketing Spend | Model 3: Multiple Regression |
|---|---|---|---|
| **Model Name** | Simple – Footfall | Simple – Marketing Spend | Multiple – Full Model |
| **Dependent Variable** | Monthly Sales | Monthly Sales | Monthly Sales |
| **Independent Variables** | Footfall | Marketing Spend | Footfall, Marketing Spend, Avg Discount %, Staff Count, Inventory Availability %, Competitor Distance, Holiday Flag, Customer Rating, Region dummies (North/South/West), Store Type dummies (Airport/High Street/Mall) |
| **R-squared** | 0.7348 | 0.1574 | 0.8550 |
| **Adjusted R-squared** | — | — | 0.8480 |
| **Significant Variables** | Footfall (p < 0.001) | Marketing Spend (p < 0.001) | Footfall, Marketing Spend, Staff Count, Inventory Availability %, Competitor Distance, Holiday Flag, Customer Rating, Region South, Region West, Region North, Store Airport, Store Mall, Store High Street |
| **Not Significant** | — | — | Avg Discount % (p = 0.373) |
| **Business Usefulness** | High — footfall is the single strongest operational lever | Moderate — marketing matters but cannot stand alone | Very High — covers all major levers: operational, structural, and location |
| **Limitations** | Ignores store type, region, inventory, competition | Very weak standalone; does not capture store structure | Multicollinearity risk; avg discount is not significant despite being included; covers only 4 months |

---

## Model 1: Simple Regression — Footfall

Footfall alone explains 73.5% of monthly sales variation (R² = 0.7348). The coefficient of 35.64 means every additional customer visit is associated with about £35.64 more in monthly sales. This is the strongest single-variable predictor in the dataset.

**Business usefulness:** High. Driving more customers into stores is directly linked to revenue. This model gives a clear, simple rule of thumb for leadership.

**Limitation:** It ignores everything else — store type, region, marketing, inventory, competition. Two stores with the same footfall but very different locations or formats can have very different sales, and this model cannot explain that difference.

---

## Model 2: Simple Regression — Marketing Spend

Marketing spend explains only 15.7% of monthly sales variation (R² = 0.1574). The coefficient of 2.05 means each extra £1 of marketing spend is associated with £2.05 more in sales — a modest positive return. The relationship is statistically significant but the explanatory power is weak.

**Business usefulness:** Moderate. Marketing clearly has some effect, but it is not the primary driver of sales. Some stores spend heavily on marketing without achieving proportionally higher sales.

**Limitation:** Marketing spend may indirectly drive sales through footfall — spending more may bring more customers, and those customers then drive sales. This indirect chain means the simple regression understates or overstates the true marketing effect. The multiple regression model separates this out more clearly.

---

## Model 3: Multiple Regression — Full Model

The full model achieves R² = 0.855 and adjusted R² = 0.848, meaning it explains 85.5% of monthly sales variation using 14 predictors. This is a substantial improvement over either simple model.

Key findings from the full model:

- **Footfall** remains the dominant driver (coefficient: £27.11 per visit, p < 0.001)
- **Inventory availability** is highly significant — each 1pp improvement adds ~£2,786 in monthly sales (p < 0.001)
- **Competitor distance** is significant and negative — stores closer to competitors tend to perform better, suggesting those locations have better footfall catchments (p < 0.001)
- **Customer rating** significantly predicts sales — each 1-point increase adds ~£12,750 (p = 0.005)
- **Marketing spend** remains significant (p < 0.001) even after controlling for footfall
- **Holiday months** generate an additional ~£14,040 on average (p = 0.023)
- **Store type** matters: Airport stores earn ~£42,600 more per month than Residential; Mall stores earn ~£30,740 more
- **Region** matters: West region stores earn ~£28,390 more than East; South earn ~£24,920 more
- **Average discount %** is the only variable not statistically significant (p = 0.373)

**Business usefulness:** Very High. Leadership can see which levers matter, how much each contributes, and where structural advantages (store type and region) create built-in sales differences that operational decisions cannot easily overcome.

**Limitation:** The large condition number (1.24e+06) signals some multicollinearity — footfall, staff count, and store size are related to each other. Individual coefficients should be read as directional guides, not precise independent effects. The dataset covers only 4 months so seasonal patterns are not fully captured.

---

## Why the Multiple Regression Model Wins

| Criterion | Winner |
|---|---|
| R-squared | Multiple Regression (0.855 vs 0.735 vs 0.157) |
| Adjusted R-squared | Multiple Regression (0.848 — confirms genuine improvement) |
| Variables covered | Multiple Regression (14 predictors across operational and structural factors) |
| Decision support | Multiple Regression (tells leadership which levers to pull) |
| Statistical strength | Multiple Regression (F-stat p < 0.001; 13 of 14 variables significant) |

**Selected final model: Multiple Regression (Full Model)**
