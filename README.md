
# Hybrid ML–Fuzzy Decision System for Investor Attractiveness

## Executive Summary

This project explores the intersection between **Machine Learning (ML)** and **Fuzzy Logic** to estimate the **attractiveness and profitability of investors** (VC firms) based on structured market and performance indicators.  
The goal was to design a **hybrid decision system** that combines quantitative prediction from ML models with qualitative reasoning using fuzzy inference — bridging algorithmic accuracy and interpretability.

Initially conceived as an **OOP-driven machine learning architecture experiment**, the project evolved into a study of **hybrid AI reasoning**, emphasizing clean modular design, transparent decision-making, and real-world applicability. At first it was intiteled Predicting-Profitable-Startups aiming to rank startups based on their profitability potential and predict their future performance to guide investment decisions.

---

## Business Problem

Evaluating venture investors’ potential is a complex task that involves both measurable and subjective factors.  
While numerical models can predict outcomes such as *market value* or *follow-on rate*, they often fail to capture the nuanced reasoning investors or analysts apply when judging “attractiveness” — such as growth potential, stage maturity, or strategic risk.

The problem addressed is therefore **twofold**:

1. How to **predict investor performance metrics** from limited, heterogeneous data.  
2. How to **translate those predictions into interpretable attractiveness scores**, closer to human reasoning.

---

## Methodology

The methodology combines **object-oriented design**, **data engineering**, and **hybrid AI reasoning** in four key stages:

### 1️. Data Collection & Preparation  
- Data was scraped from **AngelList** and augmented using **LLM-assisted feature enrichment**.  
- Custom parsers handled non-structured fields (investment stages, follow-on rates, market lists).  
- Additional engineered features (e.g., `growth_x_followon`, `risk_x_age`) were derived to simulate multi-factor investor dynamics.

### 2️. Object-Oriented ML Architecture  
The pipeline follows an extensible design inspired by software engineering principles:

- `DataPipeline` → preprocessing and feature selection (variance filtering).  
- `InvestorRegressor` → encapsulates different model types (LightGBM, Ridge).  
- `Trainer` → manages training, evaluation, and score scaling.  
- `DecisionSynthesizer` → merges ML output with fuzzy reasoning.  

This modularity demonstrates **OOP best practices in ML system design**, ensuring readability and scalability.

### 3️. Model Training and Evaluation  
- Two algorithms were tested:  
  - **Ridge Regression** → baseline, interpretable linear model.  
  - **LightGBM Regressor** → gradient boosting model effective for small tabular datasets.  
- The dataset being small, the focus was not on overfitting mitigation but on validating architectural soundness.  
- Cross-validation (5-fold) yielded an average R² ≈ **0.53 ± 0.06**, showing moderate consistency given the data constraints.

### 4️. Fuzzy Logic Integration  
- A fuzzy inference system was built with input variables such as `ml_score`, `follow_on_rate`, `stage_risk`, and `age_years`.  
- Membership functions modeled investor maturity and risk profiles.  
- Example rule:  
  `IF ml_score IS high AND follow_on IS high THEN attractiveness IS high`  
- The final decision score combined ML output and fuzzy inference:

\[
final\_score = \alpha \times ML\_prob + (1 - \alpha) \times \frac{fuzzy\_score}{100}
\]
where α = 0.6.

---

## Skills 

- **Machine Learning Engineering** — model training, feature selection, performance evaluation.  
- **OOP for AI Systems** — encapsulation of data, model, and reasoning components.  
- **Data Scraping & Augmentation** — extraction from AngelList and generation of synthetic attributes via an LLM integration.  
- **Fuzzy Logic Design** — rule-based modeling using `scikit-fuzzy`.  
- **Explainable AI (XAI)** — interpretability using **SHAP** values and feature importance plots.  
- **Hybrid Reasoning Systems** — merging statistical prediction and symbolic logic.  
---

## Results & Business Recommendation

### Model Performance
| Model | Mean R² (CV) | Test R² | RMSE |
|--------|---------------|---------|------|
| Ridge Regression | ≈ 0.48 | — | — |
| LightGBM Regressor | **0.53 ± 0.06** | **-0.57** | 133M |

Although predictive accuracy remains limited due to small data size, the **model was stable and interpretable**.

### Fuzzy Integration Outcomes
The fuzzy layer successfully transformed numeric predictions into **interpretable attractiveness categories** (Low / Medium / High).  
It provided transparent trade-offs between **risk**, **experience**, and **follow-on strength**, enabling a more explainable assessment.

### Interpretation Tools
- **SHAP** visualizations revealed that `follow_on_rate` and `market__healthcare` were the most influential features.  
- The fuzzy reasoning layer added human-like interpretability, explaining why certain investors are scored “medium attractiveness” despite moderate ML confidence.

**Business Recommendation:**  
In early-stage investor evaluation, combining ML and fuzzy reasoning allows both quantitative ranking and qualitative justification — supporting data-driven due diligence and portfolio prioritization.

---

## Next Steps

1. **Data Expansion**  
   - Increase dataset size via additional scraping or API access to VC databases.  
   - Validate model generalization on external investor datasets.

2. **Rule Refinement**  
   - Calibrate fuzzy rules with expert input or data-driven optimization of membership functions.

3. **Deployment Prototype**  
   - Convert the hybrid ML–Fuzzy pipeline into a **Streamlit** or **Dash** dashboard.  
   - Enable user interaction for adjusting α (fusion weight) and visualizing reasoning flow.

4. **Model Enhancement**  
   - Test **Bayesian** or **ensemble regressors** for uncertainty-aware predictions.  
   - Apply hyperparameter optimization (e.g., Bayesian optimization or Optuna).

---

