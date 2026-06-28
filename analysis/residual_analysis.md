# Residual Analysis

**Model used:** Multiple Regression — Full Model (R² = 0.855, 14 predictors)
**Dataset:** Clean file — 306 records

**Residual formula:** `Residual = Actual Monthly Sales − Predicted Monthly Sales`

A positive residual means the store sold more than the model expected given its characteristics.
A negative residual means the store sold less than the model expected given its characteristics.

---

## Top 5 Records with Largest Positive Residuals

These are stores the model under-predicted — they outperformed expectations.

| Store ID | Store Type | Region | Actual Sales (£) | Predicted Sales (£) | Residual (£) |
|---|---|---|---|---|---|
| STR-1058 | High Street | East | 870,937 | 759,933 | +111,005 |
| STR-1028 | Mall | East | 713,611 | 606,267 | +107,344 |
| STR-1073 | Residential | East | 813,317 | 721,217 | +92,099 |
| STR-1026 | Mall | East | 625,514 | 535,396 | +90,118 |
| STR-1051 | Airport | East | 787,716 | 700,456 | +87,260 |

### Business Interpretation

All five overperforming stores are in the **East region**. The model already accounts for regional differences through the East dummy variable baseline, so these residuals are above and beyond the expected East baseline. Possible explanations:

- **Location advantage within East:** These particular stores may sit in higher-footfall micro-locations (near transport hubs, busy high streets, or regeneration areas) that the regional dummy cannot distinguish.
- **Management quality:** Store managers or teams at these locations may be driving above-average conversion rates, upselling, or repeat visits that are not captured in any dataset variable.
- **Catchment area demographics:** Local income levels or household spending patterns in the specific catchment area may be more favourable than the regional average.
- **STR-1058 (High Street, East):** The largest positive residual. This store generates £111K more than expected — worth investigating as a potential best-practice site.

**Recommendation:** Leadership should visit these stores to understand what is working. The practices that explain their outperformance could potentially be replicated at similar-format stores in other regions.

---

## Top 5 Records with Largest Negative Residuals

These are stores the model over-predicted — they underperformed expectations.

| Store ID | Store Type | Region | Actual Sales (£) | Predicted Sales (£) | Residual (£) |
|---|---|---|---|---|---|
| STR-1023 | Mall | South | 627,172 | 765,512 | –138,340 |
| STR-1012 | Residential | West | 595,468 | 713,206 | –117,738 |
| STR-1017 | High Street | West | 685,379 | 801,191 | –115,812 |
| STR-1007 | Mall | West | 800,452 | 916,051 | –115,599 |
| STR-1060 | Mall | West | 721,079 | 808,713 | –87,633 |

### Business Interpretation

Three of the five worst-performing stores relative to expectations are **Mall stores in West region**. Given that the model predicts higher sales for both Mall formats and West region, the actual underperformance represents a meaningful gap. Possible explanations:

- **Local competition not captured:** The `competitor_distance_km` variable measures distance to the nearest competitor but says nothing about that competitor's quality, size, or brand strength. A large, well-known competitor nearby may be drawing customers away even if the distance is modest.
- **Operational problems:** Specific issues at these stores — persistent stockouts, poor layout, customer service failures — may be suppressing conversion despite favourable structural characteristics.
- **STR-1007 (Mall, West):** This store received over £172,000 in marketing spend in one month — the highest in the dataset — yet still underperforms predictions by over £115,000. High marketing spend alone cannot compensate for underlying operational or location issues.
- **STR-1023 (Mall, South):** The worst-performing store relative to predictions (–£138K gap). Given that South Mall stores should structurally perform well, this suggests store-specific issues worth investigating.

**Recommendation:** Leadership should treat these five stores as priority audit candidates. The model says they should be performing better than they are. A store operations review — covering staff quality, stock management, local competitive landscape, and customer experience — would help identify root causes.

---

## Are There Patterns in Which Stores the Model Gets Wrong?

| Pattern | Evidence |
|---|---|
| Model consistently under-predicts East stores | All 5 top positive residuals are East stores |
| Model consistently over-predicts West Mall stores | 3 of 5 largest negative residuals are West Mall or South Mall |
| High marketing spend does not fix underperformance | STR-1007 spent most on marketing yet remains a large negative residual |

The model may be giving the West region and Mall store type a higher predicted baseline than some individual stores in those categories can achieve. This could mean the West region premium (£28,390) is being driven by a subset of high-performing West stores, while others in the region lag behind the average.

---

## What These Residuals Tell Us About Model Fit

The majority of residuals fall within ±£50,000 — reasonable for stores with average monthly sales of ~£680,000. The five largest residuals in each direction fall in the £87,000–£138,000 range, which is large but not extreme relative to total sales. The model is performing well overall (R² = 0.855), and no systematic pattern suggests a fundamental flaw in the model specification. The residuals appear roughly symmetric around zero and do not show obvious clustering by store type or region beyond the East concentration in positive residuals noted above.
