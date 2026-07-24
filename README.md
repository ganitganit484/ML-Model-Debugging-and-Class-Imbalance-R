# ML-Model-Debugging-and-Class-Imbalance-R
# Model Auditing & Debugging: Logistic Regression in R

This repository contains a model audit of a naive logistic regression pipeline built to predict customer churn. 

The project demonstrates why high accuracy can be misleading in imbalanced datasets, identifies structural statistical flaws (multicollinearity and spurious correlations), and refactors the model using `tidymodels` for more reliable business insights.

## Project Workflow

### 1. Identifying Flaws in the Naive Model
* **Class Imbalance Illusion:** The original model achieved ~92% accuracy, but the dataset had an 85/15 class balance. A dummy model predicting "no churn" for every row would already yield 85% accuracy.
* **Multicollinearity:** A correlation analysis revealed strong collinearity between `tenure`, `monthly_charges`, and `total_charges` (corr = 0.85), which inflated standard errors and made individual coefficients uninterpretable.
* **Spurious Correlations:** The feature `is_tuesday_signup` showed a disproportionately large log-odds impact, indicating the model was fitting on noise rather than true causal drivers.

### 2. Model Refactoring (`tidymodels`)
* **Feature Selection & Cleaning:** Built a clean `recipe` removing redundant financial derivatives (`total_charges`) and non-causal noise (`is_tuesday_signup`).
* **Metric Shift:** Replaced raw accuracy with decision-relevant metrics: **Recall**, **Precision**, and **ROC-AUC** to properly evaluate minority class detection.

## Key Performance Results
Evaluating the refactored model on the test set:
* **Recall:** High sensitivity in identifying actual churners.
* **Precision:** Maintained low false-positive rates for churn flags.
* **Interpretability:** Coefficient weights shifted back to true business drivers, such as `contract_type` and `calls_to_support`.

## Tech Stack & Packages
* **Language:** R
* **Frameworks:** `tidymodels`, `tidyverse`, `GGally`, `vip`

## Repository Files
* `HW3_Debugging_Imbalance_Data.html` - Knitted report with complete code, plots, and statistical reasoning.
