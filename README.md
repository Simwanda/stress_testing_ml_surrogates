# \# Stress-testing ML Surrogates for Slotted Cold-Formed Steel Beams

# 

# Repository for the study:

# 

# \*\*When is a data-driven model credible? Stress-testing single and ensemble machine learning models for slotted cold-formed steel beams using local and distortional buckling benchmarks\*\*

# 

# \## Overview

# 

# This repository contains the code, analysis workflow, and reproducible artifacts used to evaluate the \*\*credibility\*\* of machine-learning surrogates for predicting the bending resistance of slotted cold-formed steel beams.

# 

# The study moves beyond conventional in-distribution accuracy and evaluates whether a model is believable for engineering use by testing it under:

# 

# \- \*\*Out-of-distribution generalization\*\*

# \- \*\*Uncertainty calibration\*\*

# \- \*\*Robustness to retraining variability\*\*

# \- \*\*Interpretability diagnostics\*\*

# 

# Two benchmark targets are considered:

# 

# \- \*\*MLB\*\*: ultimate local-buckling bending resistance

# \- \*\*MDB\*\*: ultimate distortional-buckling bending resistance

# 

# The database contains \*\*432 validated numerical samples\*\* described by geometric, perforation, and material features.

# 

# \## Why this repository matters

# 

# Many machine-learning models can achieve near-perfect performance on random train/test splits. However, high in-distribution accuracy alone does \*\*not\*\* guarantee that a model is credible for design-facing structural applications.

# 

# This repository provides a reproducible framework for checking whether a surrogate model remains reliable when exposed to realistic deployment shifts, such as:

# 

# \- new geometry regimes

# \- held-out perforation groups

# \- held-out material grades

# 

# It also evaluates whether reported uncertainty is empirically valid and whether conclusions remain stable across repeated retraining.

# 

# \## Main study components

# 

# The repository implements the following workflow:

# 

# 1\. \*\*Data preprocessing\*\*

# &nbsp;  - median imputation

# &nbsp;  - feature standardization

# &nbsp;  - leakage-safe train/test transformations

# 

# 2\. \*\*Model benchmarking\*\*

# &nbsp;  - single models:

# &nbsp;    - Ridge

# &nbsp;    - Lasso

# &nbsp;    - Elastic Net

# &nbsp;    - Decision Tree

# &nbsp;    - k-Nearest Neighbours

# &nbsp;    - Support Vector Regression

# &nbsp;    - Gaussian Process Regression

# &nbsp;  - ensemble models:

# &nbsp;    - Random Forest

# &nbsp;    - Gradient Boosted Regression Trees

# &nbsp;    - AdaBoost

# &nbsp;    - XGBoost

# &nbsp;    - LightGBM

# &nbsp;    - CatBoost

# &nbsp;    - HistGradientBoosting

# 

# 3\. \*\*In-distribution evaluation\*\*

# &nbsp;  - MAE

# &nbsp;  - RMSE

# &nbsp;  - MAPE

# &nbsp;  - R²

# 

# 4\. \*\*OOD stress testing\*\*

# &nbsp;  - \*\*Geometry shift\*\* using D/t tail regions

# &nbsp;  - \*\*Perforation shift\*\* using held-out slot-length group

# &nbsp;  - \*\*Material shift\*\* using held-out yield-strength group

# 

# 5\. \*\*Uncertainty quantification\*\*

# &nbsp;  - split conformal prediction intervals

# &nbsp;  - empirical coverage

# &nbsp;  - interval sharpness

# 

# 6\. \*\*Robustness analysis\*\*

# &nbsp;  - repeated retraining across multiple random seeds

# 

# 7\. \*\*Interpretability\*\*

# &nbsp;  - SHAP-based feature influence analysis under ID and OOD settings

# 

# \## Key findings

# 

# The main findings of the study are:

# 

# \- Several models achieve \*\*near-perfect in-distribution accuracy\*\*

# \- This strong ID performance does \*\*not\*\* necessarily transfer to OOD settings

# \- \*\*Geometry\*\* and \*\*material\*\* shifts can cause severe degradation, including large MAE inflation and negative R² for some high-performing ID models

# \- The \*\*perforation hold-out\*\* behaves more like interpolation and is handled well by most models

# \- Nominal \*\*90% conformal prediction intervals\*\* do not always achieve exact 90% empirical coverage

# \- Model rankings are broadly stable across retraining, showing that the observed credibility gaps are not due to a single lucky run

# \- SHAP diagnostics show dominant reliance on physically meaningful variables such as \*\*thickness\*\*, \*\*section depth\*\*, and \*\*yield strength\*\*

# 

# \## Repository structure

# 

# A suggested project structure is:

# 

# ```text

# stress\_testing\_ml\_surrogates/

# │

# ├── README.md

# ├── single\_ensemble\_models.ipynb

# ├── data/

# │   ├── raw/

# │   ├── processed/

# │   └── metadata/

# ├── outputs/

# │   ├── figures/

# │   ├── tables/

# │   ├── metrics/

# │   └── shap/

# ├── environment/

# │   ├── requirements.txt

# │   └── environment.yml

# └── paper/

# &nbsp;   └── credibility\_cfs.pdf

