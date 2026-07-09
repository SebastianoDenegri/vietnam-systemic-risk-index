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

## Repository Structure

```text
a_systemic_risk_framework_for_the_vietnamese_market/
├── data/                    # Datasets used throughout the project
│   ├── vsri_construction/   # Datasets used for contructing the VSRI and its risk sub-indicators
│   ├── machine_learning/    # Datasets used for training and evaluating the machine learning models
│   │   ├── ml_results/      # Parquet files with the results of the Machine Learning analysis
│   ├── appendix_c/          # Parquet files with the results of the robustness analysis
├── notebooks/               # Jupyter notebooks containing the full analysis pipeline
│   ├── A_Systemic_Risk_Framework_for_the_Vietnamese_Market_a_Composite_Risk_Index_and_Financial_Stress_Prediction.ipynb # Main notebook containing all results
│   ├── Estimating_the_Single_Company_Delta_CoVaR_for_the_Vietnam_Tail_Risk_Indicator_(VTRI).ipynb                       # Notebook for estimating Delta_CoVaRs for constructing the VTRI.
│   ├── Estimating_the_pairwise_Granger_coefficents_for_the_VGCI.ipynb                                                   # Notebook for estimating the Granger coefficents across international markets for constructing the VGCI.
│   ├── machine_learning/   # Jupyter notebooks containing the machine learning analysis
│   │   ├── Disaggregate_Sub_Indices_Predicting_Financial_Stress_Events.ipynb                    # Notebook for training and testing the ML models on the disaggregate sub indicators
│   │   ├── Stress_Proxy_Predicting_Financial_Stress_Events.ipynb                                # Notebook for training and testing the ML models on market volatility
│   │   ├── VSRI_Predicting_Financial_Stress_Events.ipynb                                        # Notebook for training and testing the ML models on the VSRI composite index
│   ├── appendix_c/         # Jupyter notebooks containing robustness analysis to verify LSTM results stability under different seeds
│   │   ├── Appendix_C1_VSRI.ipynb                                         # Notebook for traininig the LSTM network across different seeds on the VSRI composite index
│   │   ├── Appendix_C2_Disaggregated_Sub_Indices.ipynb                    # Notebook for traininig the LSTM network across different seeds on the disaggregate sub indicators
│   │   ├── Appendix_C3_Stress_Proxy.ipynb                                 # Notebook for traininig the LSTM network across different seeds on market volatility
├── README.md                # Project overview and documentation
└── requirements.txt         # Project dependencies
```
