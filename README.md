# ASD/ADHD County-Level Exposome Analysis (XAI)
Code and analysis pipeline for "Identifying environmental and socioeconomic correlates for the county-level prevalence of Autism and ADHD using Explainable Artificial Intelligence" - XGBoost + recursive feature elimination + SHAP applied to the EPA Environmental Quality Index across 3,142 U.S. counties.

# Code accompanying the manuscript:

_Identifying environmental and socioeconomic correlates for the county-level prevalence of Autism and ADHD using Explainable Artificial Intelligence_

Ria Martins, Yanni Cao, Jianyong Wu,
Division of Environmental Health Sciences, College of Public Health, The Ohio State University
Submitted to the Journal of Exposure Science & Environmental Epidemiology, 2026.

This repository contains the analysis pipeline used to identify environmental and socioeconomic correlates of county-level ASD and ADHD prevalence across 3,142 U.S. counties, using XGBoost with recursive feature elimination (RFE) and SHapley Additive exPlanations (SHAP).

# Repository structure
.
├── ASD.ipynb     # ASD analysis: XGBoost + RFE + SHAP (logit-transformed outcome)
├── ADHD.ipynb    # ADHD analysis: XGBoost + RFE + SHAP
├── requirements.txt           # Python dependencies
├── LICENSE                    # MIT License
└── README.md                  # This file

Each notebook is self-contained and produces the SHAP feature importance plots, beeswarm plots, dependence plots, and per-county dominant-predictor outputs reported in the manuscript.

# Data sources

All datasets used in this study are publicly available. They are not redistributed in this repository; please download them directly from the original sources.

Datasets were merged on county FIPS codes prior to analysis.

# Requirements

- Python 3.10 or newer
- See `requirements.txt` for the full list of package versions

Install dependencies with:

    pip install -r requirements.txt

## Core libraries

- `numpy`, `pandas` — data handling
- `scikit-learn` — cross-validation, hyperparameter search
- `xgboost` — gradient boosting regression
- `shap` — model interpretation
- `matplotlib`, `Pillow` — figures
- `jupyter` — running the notebooks

# Core libraries:

numpy, pandas — data handling
scikit-learn — cross-validation, hyperparameter search, partial dependence
xgboost — gradient boosting regression
shap — model interpretation
matplotlib, Pillow — figures

# How to reproduce

Download the three source datasets listed above.
Merge the EQI file with each prevalence file on county FIPS code, producing two CSVs (one per outcome).
Update the DATA_PATH variable at the top of each notebook to point to the merged CSV.
Run all cells. Each notebook performs:

Hyperparameter tuning via RandomizedSearchCV (5-fold cross-validation)
Recursive feature elimination in 10% increments
5-fold cross-validated performance evaluation (RMSE, R²)
SHAP-based global and local interpretation (TreeExplainer)
Generation of feature importance, beeswarm, and dependence plots

The ASD notebook additionally applies a logit transformation to the outcome before modeling.
The county-level dominant-predictor maps (Figures 4 and 5 in the manuscript) were produced in ArcGIS Pro from the per-county SHAP outputs exported by the notebooks.

# Reproducibility notes

Random seed: random_state = 42 is used throughout for cross-validation splits and stochastic estimators.
Cross-validation is non-spatial, k-fold; standard CV may overestimate generalization where neighboring counties share exposure profiles. See the manuscript Limitations section.
Feature selection and hyperparameter tuning are performed prior to the reported CV step, so reported performance metrics may be slightly optimistic relative to a fully nested validation framework.

# Citation
If you use this code, please cite the manuscript: 
Martins R, Cao Y, Wu J. Identifying environmental and socioeconomic
correlates for the county-level prevalence of Autism and ADHD using
Explainable Artificial Intelligence. Journal of Exposure Science &
Environmental Epidemiology (under review), 2026.

# License
Code in this repository is released under the MIT License. See LICENSE for details. The underlying datasets are subject to the terms of their original providers (U.S. EPA and the respective publishing journals).
