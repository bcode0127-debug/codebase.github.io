---
layout: page
title: Energy Consumption Forecasting
description: Investigating the limits of linear models at scale
img: assets/img/ensemble_diagnostics.png
importance: 2
category: Research
github: https://github.com/bcode0127-debug/energy-forecasting
related_publications: false
---

Forecasting energy demand at grid scale is harder 
than it looks. Consumption patterns shift dramatically 
between night and peak hours, and standard linear 
models struggle to keep up.

Investigated whether that gap is real and quantifiable. 
Using 167 million smart meter records from the London 
Grid, compared linear regression variants against 
gradient boosting across horizons from 30 minutes 
to 96 hours ahead.

The results were clear. Linear models plateau around 
8% improvement over baseline, gradient boosting 
reaches 15%. At 96-hour horizons, linear models 
drop below baseline entirely. Peak-hour variance 
is 2.9x higher than off-peak, and no linear variant 
including Weighted Least Squares could correct 
for it. The problem is structural, not statistical.

---

## Key Findings

Linear models hit a hard ceiling - despite optimal 
feature engineering, every linear variant plateaued 
around 8% improvement over baseline while gradient 
boosting reached 15%. More critically, linear models 
collapse below baseline at longer horizons, while 
ensemble methods remain stable throughout.

Peak-hour variance (6-9 PM) is 2.9x higher than 
off-peak. Even Weighted Least Squares failed to 
correct this, suggesting the problem is structural 
non-linearity rather than a statistical artifact.

| Model | lag_30m/24h | lag_48h/96h | Swing |
| :--- | :---: | :---: | :---: |
| Naive Baseline | 0.0% | 0.0% | - |
| OLS | +7.81% | -2.05% | -9.86% |
| Elastic Net | +8.07% | -1.72% | -9.79% |
| Huber | +7.41% | -2.59% | -10.00% |
| WLS | +4.44% | -7.11% | -11.55% |
| **GBR** | **+15.44%** | **+9.56%** | **-5.88%** |

{: .table .table-sm .table-borderless}

---

## Repository

Access the full code and documentation on [GitHub](https://github.com/bcode0127-debug/Energy_Forecasting_Project.git).



## Discussion

The interpretability trade-off is quantifiable 
an 8-10% accuracy gap that has real consequences 
in production deployment. For grid operators, a 
hybrid strategy emerges naturally from these 
results: linear models for off-peak hours where 
regulatory explainability matters, ensemble methods 
for peak hours where accuracy is critical.

This tension between performance and transparency 
connects to broader questions in ML deployment 
around model accountability in high-stakes systems.