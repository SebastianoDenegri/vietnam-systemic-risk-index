# Vietnam Systemic Risk Index (VSRI)
### A Systemic Risk Framework for the Vietnamese Market: a Composite Risk Index and Financial Stress Prediction

---
## Overview.
This repository presents a framework to quantify financial systemic risk in the Vietnamese market by developing a multi-dimensional composite index, the **Vietnam Systemic Risk Index (VSRI)**, capturing different drivers of financial vulnerability at any given point in time.

## Motivation.
The proposed analysis fills a gap in the current research on systemic risk for the Vietnamese market, where, to the best of our knowledge, a unified measure of systemic risk is still missing. The scope of the project is to establish an operational, structured framework to quantify financial systemic risk in Vietnam, providing insights on the main drivers of financial distress in a young, fast-growing, and under-studied market.

## Research Questions.
The project aims to answer the following research questions:
- Can systemic risk in a “frontier-transitioning-to-emerging” market be effectively quantified through a composite index able to capture different dimensions of financial vulnerability?
- Can this index provide predictive signals of financial stress?

## Methodology.
The proposed VSRI framework integrates five dimensions of financial risk:
- External risk spillovers.
- Domestic market fragility.
- Financial turbulence.
- Risk of downside tail co-movements.
- Market illiquidity.

We assess the contribution of each risk dimension to the overall systemic risk and we aggregate the sub-indices using a methodology inspired by the literature on composite systemic risk indices. The applied methodology integrates correlations amongst the risk drivers thus capturing the systemic nature of financial distress, where co-movements across risk dimensions correspond to heightened systemic risk.

## Results.
The empirical analysis shows that the VSRI:
- Aligns with well-known periods of financial distress in the Vietnamese market.
- Captures periods of increased systemic risk across latent market regimes.
- Brings incremental information about the buildup of risk beyond the information already contained in more conventional stress proxies.
- May contain useful signals for systemic stress prediction, potentially capturing systemic vulnerability patterns more effectively than conventional risk proxies.

Among the evaluated models (Logistic Regression, SVM, and LSTM), the LSTM trained on the VSRI achieved the strongest out-of-sample performance, reaching a recall of 75% and a ROC-AUC of 0.77.

#### Summary of all Models’ Performance

|Model Setup|Recall|F1-Score|ROC-AUC|
|---|---:|---:|---:|
|Logistic Regression (VSRI)|0.75|0.10|0.58|
|Support Vector Machines (VSRI)|0.92|0.12|0.62|
|**Long Short-Term Memory RNN (VSRI)**|**0.75**|**0.18**|**0.77**|
|Logistic Regression (Disaggregated Sub-Indices)|0.96|0.15|0.58|
|Support Vector Machines (Disaggregated Sub-Indices)|0.29|0.06|0.41|
|Long Short-Term Memory RNN (Disaggregated Sub-Indices)|0.00|0.00|0.48|
|Logistic Regression (Volatility as Stress Proxy)|0.00|0.00|0.50|
|Support Vector Machines (Volatility as Stress Proxy)|0.40|0.11|0.45|
|Long Short-Term Memory RNN (Volatility as Stress Proxy)|1.00|0.11|0.69|

The results of the study provide evidence that the VSRI can be a useful tool for Vietnamese financial regulators and policymakers, providing a rigorous framework able to quantify the current level of systemic risk, while also identifying the main drivers of systemic vulnerability, to inform risk management and financial policy decision-making.
