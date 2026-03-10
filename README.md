# Stress-testing ML Surrogates for Slotted Cold-Formed Steel Beams

Repository for the study:

**When is a data-driven model credible? Stress-testing single and ensemble machine learning models for slotted cold-formed steel beams using local and distortional buckling benchmarks**

## Overview

This repository contains the code, analysis workflow, and reproducible artifacts used to evaluate the **credibility** of machine-learning surrogates for predicting the bending resistance of slotted cold-formed steel beams.

The study moves beyond conventional in-distribution accuracy and evaluates whether a model is believable for engineering use by testing it under:

- **Out-of-distribution generalization**
- **Uncertainty calibration**
- **Robustness to retraining variability**
- **Interpretability diagnostics**

Two benchmark targets are considered:

- **MLB**: ultimate local-buckling bending resistance
- **MDB**: ultimate distortional-buckling bending resistance

The database contains **432 validated numerical samples** described by geometric, perforation, and material features.

## Why this repository matters

Many machine-learning models can achieve near-perfect performance on random train/test splits. However, high in-distribution accuracy alone does **not** guarantee that a model is credible for design-facing structural applications.

This repository provides a reproducible framework for checking whether a surrogate model remains reliable when exposed to realistic deployment shifts, such as:

- new geometry regimes
- held-out perforation groups
- held-out material grades

It also evaluates whether reported uncertainty is empirically valid and whether conclusions remain stable across repeated retraining.

## Main study components

The repository implements the following workflow:

1. **Data preprocessing**
   - median imputation
   - feature standardization
   - leakage-safe train/test transformations

2. **Model benchmarking**
   - single models:
     - Ridge
     - Lasso
     - Elastic Net
     - Decision Tree
     - k-Nearest Neighbours
     - Support Vector Regression
     - Gaussian Process Regression
   - ensemble models:
     - Random Forest
     - Gradient Boosted Regression Trees
     - AdaBoost
     - XGBoost
     - LightGBM
     - CatBoost
     - HistGradientBoosting

3. **In-distribution evaluation**
   - MAE
   - RMSE
   - MAPE
   - R²

4. **OOD stress testing**
   - **Geometry shift** using D/t tail regions
   - **Perforation shift** using held-out slot-length group
   - **Material shift** using held-out yield-strength group

5. **Uncertainty quantification**
   - split conformal prediction intervals
   - empirical coverage
   - interval sharpness

6. **Robustness analysis**
   - repeated retraining across multiple random seeds

7. **Interpretability**
   - SHAP-based feature influence analysis under ID and OOD settings

## Key findings

The main findings of the study are:

- Several models achieve **near-perfect in-distribution accuracy**
- This strong ID performance does **not** necessarily transfer to OOD settings
- **Geometry** and **material** shifts can cause severe degradation, including large MAE inflation and negative R² for some high-performing ID models
- The **perforation hold-out** behaves more like interpolation and is handled well by most models
- Nominal **90% conformal prediction intervals** do not always achieve exact 90% empirical coverage
- Model rankings are broadly stable across retraining, showing that the observed credibility gaps are not due to a single lucky run
- SHAP diagnostics show dominant reliance on physically meaningful variables such as **thickness**, **section depth**, and **yield strength**

## Repository structure

A suggested project structure is:

```text
stress_testing_ml_surrogates/
│
├── README.md
├── single_ensemble_models.ipynb
├── data/
│   ├── raw/
│   ├── processed/
│   └── metadata/
├── outputs/
│   ├── figures/
│   ├── tables/
│   ├── metrics/
│   └── shap/
├── environment/
│   ├── requirements.txt
│   └── environment.yml
└── paper/
    └── credibility_cfs.pdf
```

If your current repository is flatter than this, you can still keep this section and update it later as the project grows.

## Files currently included

- `single_ensemble_models.ipynb`  
  Main notebook containing the modelling, evaluation, OOD testing, uncertainty, and plotting workflow.

- `credibility_cfs.pdf`  
  Paper/manuscript describing the framework, methodology, results, and conclusions.

- `README.md`  
  Repository landing page.

## Methodological summary

### Input features

The benchmark dataset includes geometric, perforation, and material descriptors such as:

- section depth
- flange width
- lip width
- thickness
- slot length
- slot width
- slot spacing
- perforation descriptors
- yield strength
- root radius

### Targets

- local-buckling bending resistance
- distortional-buckling bending resistance

### Evaluation philosophy

Model credibility is assessed through three core pillars:

- **OOD generalization**
- **uncertainty validation**
- **robustness**

A practical domain-of-applicability perspective is also adopted: predictions outside the supported feature ranges should be treated cautiously rather than accepted uncritically.

## How to run

### 1. Clone the repository

```bash
git clone <your-repository-link>
cd stress_testing_ml_surrogates
```

### 2. Create an environment

Using pip:

```bash
pip install -r requirements.txt
```

Or using conda:

```bash
conda env create -f environment.yml
conda activate stress-testing-ml
```

### 3. Launch the notebook

```bash
jupyter notebook single_ensemble_models.ipynb
```

### 4. Run the workflow

Run the notebook cells in order to reproduce:

- in-distribution model benchmarking
- OOD stress-test results
- conformal prediction interval diagnostics
- robustness across seeds
- SHAP summaries
- exported plots and result tables

## Recommended dependencies

Depending on your notebook implementation, the environment will likely include:

- numpy
- pandas
- matplotlib
- scikit-learn
- xgboost
- lightgbm
- catboost
- shap
- jupyter

## Reproducibility notes

- A fixed random seed is used where stated
- Preprocessing is applied using training-set statistics only
- OOD scenarios are intentionally constructed to reflect plausible deployment shifts
- Results should be interpreted within the domain represented by the available dataset

## Citation

If you use this repository, please cite the associated paper.

**Lenganji Simwanda** 
*When is a data-driven model credible? Stress-testing single and ensemble machine learning models for slotted cold-formed steel beams using local and distortional buckling benchmarks*

## Contact

**Lenganji Simwanda**  
Klokner Institute, Czech Technical University in Prague  
Email: lenganji.simwanda@cvut.cz

## License

Add your preferred license here, for example:

- MIT License
- BSD 3-Clause License
- GNU GPL v3

If no license has been added yet, include this section as a placeholder and update it before public release.
