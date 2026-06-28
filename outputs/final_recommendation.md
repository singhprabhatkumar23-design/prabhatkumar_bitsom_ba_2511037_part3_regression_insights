# Final Business Recommendation

**Analyst:** Business Analyst
**Dataset:** business_regression_data.xlsx — 306 clean records (14 rows deleted due to missing values)
**Final Model:** Multiple Regression, R² = 0.855, Adjusted R² = 0.848
**Dependent Variable:** Monthly Sales

---

## 1. Which factors appear most strongly associated with monthly sales?

Based on the multiple regression model, the following factors have the strongest, most statistically reliable association with monthly sales:

| Factor | Coefficient | Direction | Significance |
|---|---|---|---|
| Footfall | +£27.11 per visit | Positive | p < 0.001 |
| Marketing Spend | +£1.23 per £1 | Positive | p < 0.001 |
| Inventory Availability % | +£2,786 per 1pp | Positive | p < 0.001 |
| Competitor Distance (km) | –£3,525 per km | Negative | p < 0.001 |
| Store Type: Airport | +£42,600 vs Residential | Positive | p < 0.001 |
| Store Type: Mall | +£30,740 vs Residential | Positive | p < 0.001 |
| Region: West | +£28,390 vs East | Positive | p < 0.001 |
| Region: South | +£24,920 vs East | Positive | p < 0.001 |
| Staff Count | +£3,721 per person | Positive | p = 0.002 |
| Customer Rating | +£12,750 per 1 point | Positive | p = 0.005 |
| Store Type: High Street | +£18,640 vs Residential | Positive | p = 0.001 |
| Holiday Flag | +£14,040 in holiday months | Positive | p = 0.023 |
| Region: North | +£13,670 vs East | Positive | p = 0.044 |

**Footfall is the single strongest operational lever** — it has the highest t-statistic in the model and explains 73.5% of sales variation on its own in the simple regression. All other factors contribute meaningfully but none overtakes footfall as the primary driver.

---

## 2. Which variables should leadership focus on?

**Priority 1 — Footfall**
This is the clearest and most actionable finding. More customers in the store means more sales. Leadership should invest in anything that drives store visits: loyalty programmes, click-and-collect services, local partnerships, improved signage and accessibility, and store experience improvements that encourage repeat visits.

**Priority 2 — Inventory Availability**
Each 1 percentage point improvement in inventory availability is associated with roughly £2,786 in additional monthly sales. This is a controllable operational metric. Reducing stockouts, improving replenishment speed, and maintaining adequate stock depth in high-demand categories are direct actions leadership can take with measurable expected payoff.

**Priority 3 — Customer Rating**
A 1-point improvement in average customer rating is associated with ~£12,750 more in monthly sales. While the causal chain is indirect (better service → more loyal customers → more repeat visits and spend), this finding supports investment in staff training, complaints resolution, and in-store experience.

**Priority 4 — Store Type and Format Mix**
Airport stores earn ~£42,600 more per month than Residential stores of similar characteristics. Mall stores earn ~£30,740 more. When leadership makes decisions about opening new stores, refurbishing existing ones, or prioritising capital investment, these format premiums should factor into the business case. This is a structural advantage, not an operational one — it is built into the location, not easily changed.

**Priority 5 — Marketing Spend (with ROI discipline)**
Marketing spend is significant (£1.23 return per £1 invested in the model), but the return is modest. The simple regression showed it explains only 15.7% of sales variation alone. Leadership should focus on marketing efficiency — tracking which spend actually drives footfall — rather than simply increasing the budget. The extreme case of STR-1007 (£172K marketing spend, still underperforming) illustrates the risk of over-relying on marketing without addressing operational or location factors.

---

## 3. Which variables should NOT be over-interpreted?

**Average Discount %** — This is the only variable in the full model that is not statistically significant (p = 0.373). Once all other factors are accounted for, the level of discounting does not reliably predict monthly sales in this dataset. This does not mean discounting has zero effect — it means this dataset does not provide strong evidence either way. Leadership should not expand discounting programmes based on this regression, and equally should not cut them based on the negative coefficient alone. A controlled test (A/B experiment across comparable stores) would be needed to establish the true effect.

**Competitor Distance (negative coefficient)** — The negative coefficient (–£3,525 per km) looks counterintuitive — it means stores further from competitors tend to have lower sales. Leadership should not interpret this as "move stores closer to competitors to boost sales." The explanation is almost certainly that stores near competitors are located in high-footfall urban areas that drive both higher competition density and higher sales. Distance to competitor is acting as a proxy for location quality, not as a cause of sales. It should not be used as a direct action lever.

**Staff Count** — Significant in the multiple regression (p = 0.002), but strongly correlated with store size and footfall. Adding staff to a small, low-footfall store will not necessarily generate £3,721 per person in additional sales. This coefficient should be read in context of overall store capacity and format, not used as a formula for staffing decisions.

---

## 4. What business action would you recommend?

**Immediate actions (operational, within 3–6 months):**

1. **Audit inventory availability** across all stores and set a minimum threshold target. Stores below 85% inventory availability are likely losing meaningful sales every month. This is one of the most controllable levers with a clear modelled return.

2. **Identify the five stores with the largest positive residuals** (STR-1058, STR-1028, STR-1073, STR-1026, STR-1051 — all East region) and conduct site visits to document what they are doing well. Package findings into an internal best-practice guide.

3. **Investigate the five worst-performing stores relative to predictions** (STR-1023, STR-1012, STR-1017, STR-1007, STR-1060) for specific operational or competitive issues. Do not increase marketing spend at these stores without first understanding the root cause of underperformance.

**Medium-term actions (strategic, 6–18 months):**

4. **Prioritise Airport and Mall formats** in any new site selection or expansion planning. These formats carry a structural sales premium of £30,000–£42,000 per month over Residential formats, all else equal.

5. **Invest in customer experience initiatives** — staff training, complaint resolution processes, and in-store environment improvements — to lift customer ratings. A 0.5-point improvement in average rating across the estate is associated with ~£6,375 more per store per month.

6. **Design a controlled marketing experiment.** Split comparable stores into test and control groups with different marketing spend levels and measure the actual footfall and sales impact over 2–3 months. This will give leadership a much more reliable marketing ROI estimate than the regression alone can provide.

---

## 5. What risks or limitations should leadership keep in mind?

| Risk | Detail |
|---|---|
| **Short observation window** | The dataset covers only 4 months (January–April 2025). It captures neither peak trading season (Christmas) nor the full annual sales cycle. Coefficients may shift substantially when estimated on a full year of data. |
| **Multicollinearity** | Footfall, staff count, and store size are related to each other. The model's individual coefficients cannot be treated as fully independent effects. Leadership should read them as directional signals, not precise formulas. |
| **Missing variables** | Key factors not in the dataset include: local population density, household income in catchment area, online channel performance, store age and condition, and competitor brand strength. These are likely correlated with variables in the model, creating some bias in the coefficients. |
| **14 records excluded** | The 14 rows with missing values in competitor distance or customer rating were deleted. If these records belong to a specific subset of stores (e.g., newer stores or stores in a particular region), the model results may not fully represent those stores. |
| **Residual outliers** | A handful of stores have residuals exceeding £100,000 in either direction. These are not explained by the model and warrant individual investigation before drawing conclusions. |

---

## 6. Why does regression show association but not causation?

Regression analysis identifies patterns in the data — it tells us that stores with higher footfall tend to have higher sales, and stores with better inventory availability tend to sell more. But it cannot prove that increasing footfall caused sales to rise, or that improving inventory directly caused the sales increase.

The reason is that regression cannot rule out alternative explanations:

- A store in a premium location may have both high footfall and high sales because of its location — not because footfall causes sales. Moving footfall artificially (e.g., through aggressive promotions) may not produce the same result.
- Customer rating and monthly sales may both be caused by a third factor — excellent store management — rather than rating causing sales.
- Competitor distance correlates with sales not because distance to a competitor matters, but because distance is a proxy for whether the store is in a busy urban area.

To establish causation, leadership would need controlled experiments — randomly assigning different marketing spend levels, inventory targets, or staffing levels across comparable stores, then measuring outcomes. Until that is done, the regression findings should be used to prioritise where to investigate and experiment, not as proof that a particular input directly causes a particular sales outcome.

The multiple regression model explains 85.5% of monthly sales variation and provides a strong, evidence-based starting point for decision-making. Leadership should treat it as a diagnostic tool and a basis for hypothesis testing — not as a guaranteed formula for sales improvement.
