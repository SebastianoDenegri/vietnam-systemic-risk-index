# Vietnam Systemic Risk Index (VSRI)
### A Systemic Risk Framework for the Vietnamese Market: a Composite Risk Index and Financial Stress Prediction
![Python](https://img.shields.io/badge/Python-3.12-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Google Colab](https://img.shields.io/badge/Google-Colab-F9AB00)
![License](https://img.shields.io/badge/License-MIT-green)  

**Authors:** Sebastiano Denegri and Thinh Cao  
**Institution:** WorldQuant University - MSc. Financial Engineering

---
## Publication
**Working Paper:** <a href='https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7350481'>A Systemic Risk Framework for the Vietnamese Market: a Composite Risk Index and Financial Stress Prediction</a>  
**Authors:** Sebastiano Denegri and Thinh Cao  
**SSRN:** <a href='https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7350481'>7350481</a>  
**DOI:** <a href='http://dx.doi.org/10.2139/ssrn.7350481'>http://dx.doi.org/10.2139/ssrn.7350481</a>

## Overview
This repository presents a framework to quantify financial systemic risk in the Vietnamese market by developing a multi-dimensional composite index, the **Vietnam Systemic Risk Index (VSRI)**, capturing different drivers of financial vulnerability at any given point in time.

## Motivation
The proposed analysis fills a gap in the current research on systemic risk for the Vietnamese market, where, to the best of our knowledge, a unified measure of systemic risk is still missing. The scope of the project is to establish an operational, structured framework to quantify financial systemic risk in Vietnam, providing insights on the main drivers of financial distress in a young, fast-growing, and under-studied market.

## Research Questions
The project aims to answer the following research questions:
- Can systemic risk in a “frontier-transitioning-to-emerging” market be effectively quantified through a composite index able to capture different dimensions of financial vulnerability?
- Can this index provide predictive signals of financial stress?

## Methodology
The proposed VSRI framework integrates five dimensions of financial risk:
- External risk spillovers (Vietnam Global Contagion Indicator - VGCI).
- Domestic market fragility (Vietnam Market Fragility Indicator - VMFI).
- Financial turbulence (Vietnam Financial Turbulence Indicator - VFTI).
- Risk of downside tail co-movements (Vietnam Tail Risk Indicator - VTRI).
- Market illiquidity (Vietnam Market Illiquidity Indicator - VMII).
 
```text
                  VSRI
                   ▲
                   │
 ┌────────┬────────┬────────┬────────┐
 │        │        │        │        │
VGCI     VMFI    VFTI     VTRI     VMII
```

We assess the contribution of each risk dimension to the overall systemic risk and we aggregate the sub-indices using a methodology inspired by the literature on composite systemic risk indices. The applied methodology integrates correlations amongst the risk drivers, thus capturing the systemic nature of financial distress, where co-movements across risk dimensions correspond to heightened systemic risk.  

To evaluate the predictive usefulness of the VSRI, we formulate a binary financial stress prediction task, where financial stress events are defined as the
lowest 5th percentile of the empirical distribution of the Vietnamese market cumulative returns over a period of 20 days. Three alternative feature specifications are compared:
- The VSRI.
- The five disaggregated VSRI sub-indices.
- Market volatility alone as a conventional stress proxy.

We evaluate Logistic Regression, Support Vector Machines (SVM), and Long Short-Term Memory (LSTM) networks under each specification using out-of-sample performance.

## Research Architecture
```text
┌──────────────────┐
│  Data Gathering  │
└──────────────────┘
         │
         ▼
┌──────────────────┐
│   Data Cleaning  │
│      & EDA       │
└──────────────────┘
         │
         ▼
┌──────────────────┐
│    Five Risk     │
│    Dimensions    │
└──────────────────┘
         │
         ▼
┌──────────────────┐
│ Composite Index  │
│       VSRI       │
└──────────────────┘
         │
         ▼
┌──────────────────┐
│   VSRI Economic  │
│    Validation    │
└──────────────────┘
         │
         ▼
┌──────────────────┐
│   ML Analysis &  │
│    Prediction    │
└──────────────────┘
         │
         ▼
┌──────────────────┐
│ LSTM Sensitivity │
│     Analysis     │ 
│   (Appendix C)   │
└──────────────────┘
```

## Results
The empirical analysis shows that the VSRI:
- Aligns with well-known periods of financial distress in the Vietnamese market.  
- Captures periods of increased systemic risk across latent market regimes.
- Brings incremental information about the buildup of risk beyond the information already contained in more conventional stress proxies.
- May contain useful signals for systemic stress prediction, potentially capturing systemic vulnerability patterns more effectively than conventional risk proxies.

<img src="images/vsri_timeline.png">
<p align="center">
<em>Figure 1. Vietnam Systemic Risk Index (VSRI) over time. Peaks correspond to periods of financial stress in the Vietnamese market.</em>
</p>

The LSTM network trained on the VSRI achieved the strongest out-of-sample performance, reaching a **recall of 75%** and a **ROC-AUC of 0.77**, showing that the composite VSRI provides more informative predictive features than either its individual sub-indices or market volatility alone.

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

Because neural networks are sensitive to random initialization, in Appendix C we perform a robustness check to verify whether the LSTM results are stable under different random seeds. The empirical findings show that the performance of the LSTM trained on market volatility tends to be quite unstable across the seeds, whilst the LSTM network trained on the VSRI shows generally stronger and more consistent performance metrics.

The results of the study provide evidence that the VSRI can be a useful tool for Vietnamese financial regulators and policymakers, providing a rigorous framework able to quantify the current level of systemic risk, while also identifying the main drivers of systemic vulnerability, to inform risk management and financial policy decision-making.

## Repository Structure

```text
vietnam-systemic-risk-index/
├── data/                    
│   ├── vsri_construction/                    # Datasets for constructing the VSRI
│   ├── machine_learning/                     # Datasets for the machine learning analysis
│   │   └── ml_results/                       # Machine learning results
│   └── appendix_c/                           # Robustness analysis results
├── images/                                   # Charts and figures
├── notebooks/               
│   ├── vsri_framework.ipynb                  # Main notebook with all results
│   ├── estimate_delta_covar.ipynb            # Single-company Delta CoVaRs estimation
│   ├── estimate_granger.ipynb                # Pairwise Granger coefficients estimation across international markets
│   ├── machine_learning/                     # Notebooks for machine learning analysis
│   └── appendix_c/                           # Notebooks for robustness analysis
├── LICENSE                                   # MIT license
├── README.md                                 # Project overview and documentation
└── requirements.txt                          # Python dependencies
```
The main entry point for reproducing the study is the notebook `vsri_framework.ipynb`, which contains the complete implementation of the VSRI framework and reproduces all the results presented in this repository. The remaining notebooks contain supporting analyses used to estimate the Delta CoVaRs and Granger coefficients required to construct two of the VSRI sub-indices, perform the machine learning experiments, and conduct the LSTM robustness check.  
Each subdirectory under `data/` contains a dedicated README.md describing its contents.

## Installation
No local installation is required. The notebooks were developed and tested using **Google Colab**.
To reproduce the analysis:
1. Clone or download this repository.
2. Open the desired notebook, from the `notebooks/` directory, in Google Colab.
3. Run the notebook.
4. When prompted, **decline the Google Drive connection request** and upload the requested dataset from the repository's `data/` directory.

To reproduce the complete study using `vsri_framework.ipynb`, the required datasets are located in the `data/vsri_construction/` and `data/machine_learning/ml_results/` directories.

## Usage
The main notebook reproducing the complete study is: `notebooks/vsri_framework.ipynb`

Supporting notebooks include:
- `notebooks/estimate_granger.ipynb` – Estimation of pairwise Granger coefficients across international markets required for the computation of the Vietnam Global Contagion Indicator (VGCI).
- `notebooks/estimate_delta_covar.ipynb` – Estimation of single-company Delta_CoVaRs required for the computation of the Vietnam Tail Risk Indicator (VTRI).
- `notebooks/machine_learning/` – Notebooks for the financial stress prediction ML analysis. 
- `notebooks/appendix_c/` – Notebooks for the LSTM robustness analysis across different random initializations.

Each notebook will prompt the user to upload the required datasets from the corresponding folder under `data/`.

## Citation
If you use the VSRI framework, methodology, or any part of the code from this repository in academic work, research, or other projects, please cite this study and acknowledge the original authors:  
> Denegri, Sebastiano and Thinh Cao. "A Systemic Risk Framework for the Vietnamese Market: a Composite Risk Index and Financial Stress Prediction." *SSRN*, 2026. http://dx.doi.org/10.2139/ssrn.7350481.

## License
This project is licensed under the MIT License. See the <a href='https://github.com/SebastianoDenegri/vietnam-systemic-risk-index/blob/main/LICENSE'>`LICENSE`</a> file for details.  
If you use the VSRI framework, methodology, or any part of the code from this repository in academic work, research, or other projects, please cite this study as described in the **Citation** section.

## Acknowledgments
- WorldQuant University and the MSc in Financial Engineering program.
- <a href='https://cafef.vn/'>CafeF</a>, <a href='https://finance.yahoo.com/'>Yahoo Finance</a>, and <a href='https://github.com/akfamily/akshare'>AKShare</a> for providing access to the data used in this research.
- The Python community and the developers of the open-source libraries used to develop the VSRI framework.
