# US Crime Rate Modeling: Comparing Regression, Regularization, and Tree-Based Methods

## Overview
This project demonstrates the design, evaluation, and comparison of **regression and machine learning models** to predict US crime rates using socio-economic indicators. The analysis focuses on proper model validation, generalization performance, and methodological rigor rather than maximizing in-sample fit.

The project is structured as an end-to-end **crime rate modeling pipeline**, covering data overview, outlier assessment, baseline regression, dimensionality reduction, regularization techniques, and tree-based methods.  

A central theme of this work is **robust model selection**: ensuring that predictions are interpretable, stable, and reflective of true out-of-sample performance.

## Business Problem
Predicting crime rates at the city level is important for public policy, resource allocation, and socio-economic planning:

- Identify socio-economic drivers of crime  
- Forecast crime rates for resource planning  
- Ensure models generalize to new cities rather than overfitting historical data  

The goal is to develop models that balance predictive accuracy, interpretability, and robustness under data limitations.

## Data Source
- **US Crime Dataset**  
  Public dataset from the **UCI Machine Learning Repository** 
  http://www.statsci.org/data/general/uscrime.html 

**Dataset characteristics:**
- 47 observations (cities)
- 15 numeric predictors (socio-economic variables)
- 1 numeric response variable (`Crime`)

## Tech Stack
- **Language:** R  
- **Environment:** RStudio  
- **Key Libraries:**  
  - `DAAG` (Cross-validation)  
  - `tree` (Regression Trees)  
  - `randomForest` (Random Forests)  
  - `glmnet` (Ridge, Lasso, Elastic Net)  
  - `outliers` (Grubbs’ Test)

## Methodology

### 1. Data Overview and Outlier Assessment
- Explored distributions, outliers, and normality of the response variable (`Crime`)  
- Applied Grubbs’ test to detect high- and low-end outliers  
- Found two high-end values of interest but retained the full dataset due to small sample size  
- Scaling decisions deferred to downstream modeling where needed

### 2. Baseline Linear Regression
- **Full model:** all predictors; high in-sample R² (~0.80) but poor cross-validated performance (~0.42), indicating overfitting  
- **Reduced model:** only significant predictors (M, Ed, Po1, U2, Ineq, Prob); improved generalization (CV R² ~0.63) and interpretability  
- Predictions made on example test cases to assess plausibility

### 3. Principal Component Regression (PCR)
- Applied PCA to standardized predictors to address multicollinearity  
- Retained first five components (~86% variance explained)  
- Regression on principal components stabilized coefficients but did **not** improve cross-validated performance relative to reduced linear regression  
- Concluded PCR is useful for robustness checks, not primary prediction

### 4. Regularization Models
- Stepwise regression, Ridge, Lasso, and Elastic Net applied to control overfitting and multicollinearity  
- Lasso and Elastic Net produced sparse, interpretable models  
- Regularization improved stability but did not outperform the reduced linear regression in predictive accuracy

### 5. Tree-Based Models
- Regression trees captured non-linear interactions but were sensitive to pruning  
- Random forests reduced variance and slightly improved test RMSE (~355 vs. ~371 for pruned tree)  
- Key predictors identified: Po1, Po2, Ineq, Prob  
- Ensemble methods improved predictive stability at the expense of interpretability

## Key Insights
- Simpler, interpretable models generalized better than complex or highly flexible models  
- Multicollinearity exists but can be mitigated without aggressive dimensionality reduction  
- Cross-validation is essential for detecting overfitting, particularly in small datasets  
- Tree-based models provide complementary insights into interactions and nonlinear effects

## Limitations and Future Work
- Small sample size (n=47) limits flexibility and stability of complex models  
- Results sensitive to data splits and model hyperparameters  
- Analysis focused on prediction, not causal inference  
- Future work could explore:
  - Larger datasets or repeated cross-validation  
  - Bayesian frameworks to quantify uncertainty  
  - Integration of external socio-economic data

## Repository Structure

```
us-crime-rate-modeling/
├── data/
│ └── uscrime.txt

├── notebooks/
│ ├── 01_data_overview_and_outlier_assessment.Rmd
│ ├── 02_regularization_models.Rmd
│ ├── 03_pca_regression.Rmd
│ ├── 04_baseline_regression.Rmd
│ └── 05_tree_based_models.Rmd
│ └── 06_model_synthesis_and_final_conclusions.Rmd

├── docs/
│ ├── index.html
│ ├── 01_data_overview_and_preparation.html
│ ├── 02_regularization_models.html
│ ├── 03_pca_regression.html
│ ├── 04_baseline_regression.html
│ └── 05_tree_based_models.html
│ └── 06_model_synthesis_and_final_conclusions.html

├── README.md
└── .gitignore

## Notes
- All modeling decisions prioritize **interpretability, robustness, and reproducibility**  
- Reported test and CV results represent unbiased estimates of out-of-sample performance  
- No data points were removed; outliers were assessed but retained due to small sample size
```

---

## Contact
- **Name:** Catalina Valencia
- **Email:** catalinavalenciad@gmail.com
- **LinkedIn:** https://www.linkedin.com/in/catalina-valencia/
