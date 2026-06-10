# Citation Map — TT3L_G08 Notebook

Complete audit of every reference: where in the notebook it appears, what claim it supports, and what the source paper actually says. Use this for the viva — you can defend every citation.

---

## Quick summary

| # | Reference | Used in | Required? |
|---|---|---|---|
| 1 | Apergis & Payne (2010) | §1.2 · §9 Q2 · §10.3 | ✅ load-bearing |
| 2 | IEA (2021) | §1.2 · §9 Q1 · §9 Q2 · §9 Q3 · §10.2 | ✅ heavily used |
| 3 | Onukwulu et al. (2021) | §10.4 | ✅ future-work citation |
| 4 | Owusu & Asumadu-Sarkodie (2016) | §1.2 · §9 Q1 · §9 Q2 · §10.2 | ✅ heavily used |
| 5 | Ritchie & Roser (2022) | §1.2 · §9 Q3 · §10.3 | ✅ biomass-classification claim |
| 6 | United Nations (2015) | §1.2 · §10.4 | ✅ defines SDG 7 framework |
| 7 | Yu, Zhu & Tian (2021) | §10.2 | ✅ supports segmented policy framing |
| 8 | Tanwar (2023) — Kaggle | README · §2 | ✅ dataset attribution (required) |
| 9–14 | Libraries (NumPy etc.) | — (used in every code cell) | ⚠️ Optional but recommended |

---

## 1. Apergis, N., & Payne, J. E. (2010)

**Full citation:** Renewable energy consumption and economic growth: Evidence from a panel of OECD countries. *Energy Policy, 38*(1), 656–660. https://doi.org/10.1016/j.enpol.2009.09.002

### Where cited
- **§1.2 Background & Context**
  > *"Apergis and Payne (2010) demonstrated a bidirectional causal relationship between renewable energy consumption and economic growth across OECD countries, suggesting that the two processes are mutually reinforcing over the long run."*
- **§9 Q2 — Multiple Linear Regression** (Finding #1)
  > *"This is consistent with Apergis & Payne (2010) and the IEA (2021): higher income brings higher energy demand and, in most countries, more fossil-fuel use."*
- **§10.3 Limitations**
  > *"Apergis and Payne (2010) document a bidirectional renewable–GDP relationship that linear models cannot resolve."*

### Why we cite it
The paper establishes the **bidirectional causality** between renewable energy and economic growth in OECD countries. We use this:
1. To frame the literature gap in §1
2. To support our Q2 finding that GDP drives emissions
3. To justify the §10 limitation that our linear model cannot resolve causality direction

---

## 2. International Energy Agency (IEA). (2021)

**Full citation:** *World Energy Outlook 2021*. IEA Publications. https://www.iea.org/reports/world-energy-outlook-2021

### Where cited
- **§1.2 Background**
  > *"the International Energy Agency (IEA, 2021) documents persistent heterogeneity in energy profiles across income levels, with high-income nations exhibiting higher absolute renewable capacity but not necessarily higher renewable shares, partly due to the classification of traditional biomass as renewable in international accounting frameworks."*
- **§9 Q1** — supports the biomass interpretation of the negative GDP↔renewable correlation
- **§9 Q2** — supports the wealth-dominates-emissions finding
- **§9 Q3** — supports the renewable-share-paradox interpretation
- **§10.2 Overall Insight** — co-cited with Owusu

### Why we cite it
The IEA report is the **authoritative international source** for the *biomass classification* claim — which is the central interpretive insight of the whole project (it explains why renewable share is misleading for low-income countries). This citation underpins findings in Q1, Q2, Q3, and the Conclusion.

---

## 3. Onukwulu, E. C., Agho, M. O., & Eyo-Udo, N. L. (2021)

**Full citation:** Framework for sustainable supply chain practices to reduce carbon footprint in energy. *Open Access Research Journal of Science and Technology, 1*(2), 12–34. https://doi.org/10.53022/oarjst.2021.1.2.0032

### Where cited
- **§10.4 Implications & Future Work**
  > *"Sectoral analysis. Extend to firm-level data on sustainable supply chain practices (Onukwulu et al., 2021) to bridge the gap between national emissions targets and operational decarbonisation."*

### Why we cite it
Used **only in the future-work section** to motivate a sectoral extension. The paper proposes a framework for sustainable supply chain practices — we cite it as a methodological pointer for extending our national-level analysis to firm-level decarbonisation work. Not load-bearing for our main findings.

---

## 4. Owusu, P. A., & Asumadu-Sarkodie, S. (2016)

**Full citation:** A review of renewable energy sources, sustainability issues and climate change mitigation. *Cogent Engineering, 3*(1), 1167990. https://doi.org/10.1080/23311916.2016.1167990

### Where cited
- **§1.2 Background**
  > *"Owusu and Asumadu-Sarkodie (2016) identified institutional and financial barriers as primary constraints on renewable adoption in lower-income countries, irrespective of technological progress."*
- **§9 Q1** — supports the biomass-confounding interpretation of the negative correlation
- **§9 Q2 (Finding #3)**
  > *"Higher installed renewable capacity per capita is associated with slightly lower per-capita CO₂, but the effect is modest. This matches Owusu & Asumadu-Sarkodie (2016): installed capacity alone does not displace fossil emissions unless paired with policy and grid integration."*
- **§10.2 Overall Insight** — co-cited with IEA

### Why we cite it
The paper documents the **institutional barriers** to renewable adoption in low-income countries. We use it:
1. To establish the literature gap in §1
2. To explain why installed renewable *capacity* (Q2 predictor) has a small effect — installed hardware ≠ deployed displacement of fossils

---

## 5. Ritchie, H., & Roser, M. (2022)

**Full citation:** *Energy*. Our World in Data. https://ourworldindata.org/energy
*(Our World in Data is an Oxford-affiliated data visualisation and analysis platform.)*

### Where cited
- **§1.2 Background**
  > *"Ritchie and Roser (2022), who show that electricity access and per capita energy consumption are strongly positively correlated with GDP per capita, thereby complicating straightforward comparisons of renewable share across income groups."*
- **§9 Q3 Interpretation (Finding #2)** — co-cited with IEA on biomass classification
- **§10.3 Limitations**
  > *"International accounting (Ritchie & Roser, 2022) classifies traditional biomass as renewable. This inflates renewable-share metrics for low-income countries and is the root cause of the negative Q1 correlation."*

### Why we cite it
This is the **secondary scholarly source** for the biomass-classification claim (IEA is primary). We also cite it for the §1 framing that GDP–electricity-access correlation complicates cross-country comparisons of renewable share. Together with the IEA citation, this gives the biomass-classification claim very strong backing.

---

## 6. United Nations. (2015)

**Full citation:** *Transforming our world: The 2030 Agenda for Sustainable Development* (A/RES/70/1). United Nations General Assembly. https://sdgs.un.org/2030agenda
*(The foundational document defining the 17 SDGs, including SDG 7 — Affordable & Clean Energy.)*

### Where cited
- **§1.1 Main Objective** & **§1.2 Background**
  > *"contribute to global progress towards Sustainable Development Goal 7 (SDG 7) — Affordable and Clean Energy."*
  > *"the commitments established under the 2030 Agenda for Sustainable Development (United Nations, 2015)"*
- **§10.4 Implications**
  > *"Sustainable Development Goal 7 monitoring (United Nations, 2015) would benefit from cluster-specific sub-targets."*

### Why we cite it
The UN SDG document is the **policy framework** within which the entire problem statement sits. Without this citation, the §1 claim about "contributing to SDG 7" is unsupported. We also cite it in §10.4 to propose policy refinements.

---

## 7. Yu, Y., Zhu, W., & Tian, Y. (2021)

**Full citation:** Green supply chain management, environmental degradation, and energy: Evidence from Asian countries. *Discrete Dynamics in Nature and Society, 2021*, Article 5179964. https://doi.org/10.1155/2021/5179964

### Where cited
- **§10.2 Overall Insight**
  > *"The cross-country evidence on green energy practices reported by Yu et al. (2021) supports this segmented framing."*

### Why we cite it
The paper is a **cross-country Asian study** on the relationship between green supply chain practices, environmental degradation, and energy. We cite it to support the §10 claim that segmented (cluster-specific) policy is warranted, because the Yu et al. cross-country analysis shows that policy effectiveness differs across country profiles.

---

## 8. Tanwar, A. (2023) — Dataset

**Full citation:** *Global Data on Sustainable Energy (2000–2020)* [Data set]. Kaggle. https://www.kaggle.com/datasets/anshtanwar/global-data-on-sustainable-energy

### Where cited
- **README**, **§2 Data Source & Understanding**

### Why we cite it
The dataset attribution is **mandatory** per the rubric — the examiner will download from the link provided. Tanwar is the Kaggle uploader who aggregated this dataset from World Bank, IEA, and Our World in Data sources.

---

## Software & Libraries (NumPy, Matplotlib, pandas, scikit-learn, SciPy, seaborn)

### Where cited
- Listed in **References § Software & libraries** subsection only
- **NOT** explicitly cited in body text

### Do we need them?

**Honest answer: not required by the rubric, but recommended.**

| Argument to keep | Argument to remove |
|---|---|
| Gives credit to FOSS authors — academic norm | Rubric doesn't require it |
| Some lecturers expect it | Adds 6 lines to References |
| Matches the team's existing professional presentation | Body text doesn't say "we used pandas (McKinney, 2010)" |

### Recommendation: **KEEP**

- Every code cell uses these libraries — without them no analysis is possible
- The 6 citations take only 6 lines
- It's a **safe default** — including them never costs marks, omitting them *might* (lecturer-dependent)
- It signals academic literacy / awareness of open-source citation norms

If you want a leaner notebook for stylistic reasons, dropping the Libraries section is also defensible. Either choice is rubric-safe.

---

## Notes on prior removals

These references were briefly added and then removed during the citation cleanup. Recording them here for transparency in case a reviewer asks.

| Reference | Reason removed |
|---|---|
| Ashraf & Javed (2025) | Group could not access the paper through institutional login — academic integrity rule: don't cite what you haven't read |
| Evans, J. D. (1996) | Only used for a verbal-strength scale; we now describe the |r| thresholds in our own words in §8.1.3 — no attribution needed |
| Nouwe Edou & Onwudili (2022) | Was never cited in body text; topic (biohydrogen buses, West Midlands) is too far from our cross-national energy analysis |
| Yildiz Çankaya & Sezen (2019) | Journal website inaccessible to the group; could not verify the paper |

---

## Final integrity check

| Check | Status |
|---|---|
| Every reference is cited at least once in the text | ✅ |
| Every in-text citation has a matching reference | ✅ |
| All academic claims are backed by a cited source | ✅ |
| No "padded" citations (sources we never read or used) | ✅ |
| DOIs verified clickable | ✅ |
| Dataset citation present | ✅ |
| §1.2 UN citation consistent with reference (2030 Agenda, not Paris Agreement) | ✅ |

**You can defend every citation in the viva.** Each one supports a specific claim you make — there are no decorative references.
