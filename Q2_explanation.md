# Q2 — Multiple Linear Regression: Explanation

> **Research question:** To what extent do renewable energy capacity and energy intensity predict CO₂ emissions across countries over time?

This document explains every choice made in Q2 so you (or any group member) can defend the analysis during the viva / recorded presentation.

---

## 1. Why Multiple Linear Regression (MLR)?

The question has three signals that point to MLR:

| Question signal | What it implies | MLR fit? |
|---|---|---|
| "to what extent … predict …" | Need a quantified *effect size* and *explained variance* | ✅ R² + coefficients |
| "renewable capacity **and** energy intensity" | More than one predictor → need *partial effects* | ✅ MLR is built for this |
| CO₂ emissions (a continuous number) | Need a regression, not a classifier or cluster | ✅ Linear regression target |

MLR is also distinct from the other three questions (Q1 = correlation, Q3 = clustering, Q4 = classification), so the rubric criterion "four distinct techniques" is satisfied.

---

## 2. Target variable — why `log₁₀(CO₂ per capita)`?

Two transformations are stacked, each with a reason from EDA:

### 2.1 Per-capita instead of total kt
- **Reason:** raw CO₂ in kilotonnes is dominated by country *size*. China + USA + India contribute ~50% of global emissions just because they have huge populations.
- If we predicted raw kt, the model would mostly learn "is this country big?" — not "what energy patterns drive emissions?"
- §5.3 EDA already showed this: top-5 emitters carry the bulk of the distribution.
- Per-capita CO₂ (tonnes per person) removes the size effect so the predictors can actually explain pattern, not scale.

### 2.2 log₁₀ transform
- **Reason:** CO₂ per capita is still right-skewed (Qatar ≈ 35 t/person vs. Burundi ≈ 0.05 t/person — three orders of magnitude apart).
- §5.2 EDA already plotted raw vs. log CO₂ and showed log is approximately symmetric.
- Symmetric residuals → linear regression's assumptions hold (homoscedasticity, normal residuals, linearity).
- log₁₀ also gives a nicer interpretation: a 1-unit change in `log_co2` = a 10× change in actual CO₂.

**Combined:** `log₁₀(CO₂ per capita)` is the cleanest target — normalised for country size and symmetric in distribution.

---

## 3. Predictors

### Focal predictors (the question literally asks about these)
| Variable | Meaning |
|---|---|
| `renewable_capacity_per_capita` | Installed renewable electricity-generating capacity per person (W/person) |
| `energy_intensity` | Energy required to produce $1 of GDP (MJ/$2017 PPP) — lower = more efficient |

### Control variables (added to avoid biased coefficients)
| Variable | Why include it |
|---|---|
| `log₁₀(gdp_per_capita)` | Wealthier countries emit more — without controlling for wealth, our "renewable" coefficient would be confounded by the fact that rich countries both invest in renewables and emit more |
| `energy_consumption_per_capita` | Total energy demand drives emissions independently of how that energy is sourced |

### Excluded by design (leakage)
§5.11 EDA explicitly flagged these as mechanically tied to CO₂:
- `electricity_fossil_twh`, `electricity_renewable_twh`, `electricity_nuclear_twh` — these literally *sum* to total electricity output, so including them would let the model "cheat"
- `low_carbon_electricity_pct` — derived from the same TWh columns
- `renewable_share_pct` — definitionally overlaps with renewable capacity

Including any of these would inflate R² artificially and the coefficients would be meaningless.

---

## 4. Train / Test split — why `GroupShuffleSplit` by country?

This is the most subtle part of Q2.

**Problem with a normal random split:** the dataset is a *panel* — each country appears in 21 different rows (one per year, 2000–2020). If we did a normal random 80/20 split:
- The same country (say Norway) might appear in both train and test, just in different years
- The model would learn "Norway always has low CO₂ per capita" rather than the *general relationship* between predictors and emissions
- Test R² would look artificially high — it's just memorising country identities

**Solution: `GroupShuffleSplit` with `groups=country`.**
- Splits at the country level, not the row level
- 94 countries go into train, 24 entirely separate countries go into test
- Country overlap between sets = 0 (we print this to verify)
- Test R² now genuinely measures how well the model generalises to *countries it has never seen*

This is the standard practice in panel-data ML — required by your §5.11 EDA notes.

---

## 5. Why `StandardScaler` on the features?

Without scaling, the coefficient on `renewable_capacity_per_capita` (measured in W/person, possibly 0–500) is not comparable to the coefficient on `energy_intensity` (measured in MJ/$, possibly 0–20). One predictor's "unit" is much bigger than another's, so raw β values mean nothing for ranking.

After `StandardScaler` (fit on train only, then applied to test):
- Every predictor has mean 0 and SD 1
- Each β answers: **"how does log CO₂ per capita change when this predictor moves 1 standard deviation, holding the others fixed?"**
- |β| values are now directly comparable → we can rank which predictor matters most

We fit the scaler **on training data only** to avoid data leakage from the test set.

---

## 6. What the coefficient table tells us

After running the model:

| Predictor | β (standardised) | Direction | What it means |
|---|---|---|---|
| `log_gdp` | **+0.67** | ↑ CO₂ | A 1 SD richer country emits 0.67 SD more log CO₂ per capita — **dominant driver** |
| `energy_intensity` | +0.12 | ↑ CO₂ | Inefficient countries emit more, after wealth is controlled for |
| `renewable_capacity_per_capita` | −0.03 | ↓ CO₂ | Higher renewable capacity slightly lowers emissions — small effect |
| `energy_consumption_per_capita` | −0.02 | ≈ 0 | Effect absorbed by `log_gdp` (multicollinear) |

**Key takeaway:** wealth (`log_gdp`) is by far the biggest force pushing emissions up; energy efficiency (`energy_intensity`) is the biggest policy-controllable lever pushing them down; renewable capacity alone is *not* a strong driver in linear terms — consistent with Owusu & Asumadu-Sarkodie (2016).

---

## 7. What the metrics tell us

| Metric | Train | Test | Interpretation |
|---|---|---|---|
| **R²** | ~0.82 | ~0.81 | The 4 predictors explain ~81% of variation in log CO₂ per capita across countries — strong model |
| **RMSE** | ~0.30 | ~0.31 | Typical prediction error is 0.31 in log₁₀ units → factor of 10^0.31 ≈ 2× in actual CO₂ |
| **MAE** | ~0.23 | ~0.24 | Median absolute error similar |

**Train ≈ Test → not overfitting.** A small gap means the model generalises to the 24 entirely unseen countries.

---

## 8. What the three diagnostic plots show

### (1) Coefficient bar chart
- Horizontal bars, sorted by magnitude
- Green = negative effect (reduces CO₂), red = positive effect (increases CO₂)
- Visually confirms log_gdp dominates; everything else is much smaller

### (2) Predicted vs Actual (test set)
- Each point = one country-year in the test set
- Red dashed line = 45° (perfect prediction)
- Points clustered tightly along the line → good fit
- Points scattered far → model misses that country-year

### (3) Residuals vs Predicted
- Residual = actual − predicted (vertical distance from 45° line)
- Should look like a **random cloud around y = 0** if assumptions hold
- A *fan shape* would mean heteroscedasticity (variance changes with magnitude) — violation
- A *curve* would mean non-linearity — violation
- Our plot is approximately random around 0 → assumptions OK

---

## 9. How this links back to the problem statement

The overall project asks: *"How do economic development and energy consumption patterns influence renewable energy adoption and carbon emissions globally between 2000 and 2020?"*

Q2's contribution:
1. **Economic development** (GDP per capita) is the strongest force pushing emissions up — quantified at β = +0.67
2. **Energy intensity** (a proxy for efficiency) is the strongest *modifiable* lever — β = +0.12
3. **Renewable capacity** by itself has a small linear effect — installed hardware does not automatically displace fossil fuels (matches Owusu & Asumadu-Sarkodie 2016)
4. **Policy implication:** to reduce emissions globally, focus on energy intensity (efficiency) and on policies that translate renewable *capacity* into renewable *displacement* of fossil fuels — not just on installation targets

This sets up Q3 (clustering — *what country profiles emerge from these patterns?*) and Q4 (classification — *can we predict electricity access from these same drivers?*).

---

## 10. Likely viva questions + short answers

| Q | Short answer |
|---|---|
| Why log + per-capita target? | Per-capita removes size bias; log symmetrises the heavy right-skew documented in EDA §5.2 |
| Why GroupShuffleSplit? | Prevents country leakage across train/test in a panel dataset (§5.11) |
| Why StandardScaler? | Makes |β| values comparable so we can rank predictors |
| Why exclude renewable_share_pct? | It's definitionally overlapping with renewable_capacity_per_capita and electricity-source TWh columns — leakage |
| Why is `energy_consumption_per_capita` β nearly zero? | It's highly correlated with `log_gdp` (r ≈ 0.65) — wealth absorbs most of its signal. VIF still <5 so not problematic |
| R² = 0.81 — is that high? | Yes, for cross-country economic data with held-out countries this is strong. 81% of variance explained without overfitting (train-test gap < 0.01) |
| What's the biggest weakness? | Linear functional form may miss interactions (e.g. renewables matter more in countries with high grid quality); see "future work" in Conclusions |

---

## 11. References used in this analysis
- Apergis, N., & Payne, J. E. (2010). Renewable energy consumption and economic growth: Evidence from a panel of OECD countries. *Energy Policy*, 38(1), 656–660.
- Owusu, P. A., & Asumadu-Sarkodie, S. (2016). A review of renewable energy sources, sustainability issues and climate change mitigation. *Cogent Engineering*, 3(1), 1167990.
- IEA (2021). *World Energy Outlook 2021*.
