# 📊 Credit Portfolio Risk Modelling & Vasicek Framework

This project builds an end-to-end **loan-level credit risk modelling pipeline**, connecting borrower-level models (PD, LGD, EAD) with **portfolio-level risk analysis** using the Vasicek single-factor framework.

The objective is to replicate a simplified but **industry-aligned Basel-style credit risk workflow**, from data preparation to expected loss and correlation modelling.

---

# 🎯 Project Objective

The project develops a structured credit risk framework that:

* Estimates **Probability of Default (PD)** using Logistic Regression
* Models **Loss Given Default (LGD)** using a two-stage approach
* Estimates **Exposure at Default (EAD)** using a CCF-based regression
* Computes **Expected Credit Loss (ECL = PD × LGD × EAD)** at loan level
* Estimates **asset correlation (ρ)** using the Vasicek framework

It bridges **retail credit modelling techniques** with **portfolio credit risk theory** used in Basel IRB approaches.

---

# 📂 Dataset

**Source:** Lending Club Loan Dataset

The dataset includes:

* Loan amount, term, interest rate
* Borrower characteristics
* Loan status (Fully Paid / Charged Off / Current)
* Recovery and exposure variables

### 🎯 Target Definition

* Charged Off → **Default = 1**
* Fully Paid → **Default = 0**
* Loans with status *Current* are excluded

⚠️ Dataset is not included due to GitHub size limits.

---

# 📂 Project Structure

```
credit-portfolio-vasicek-simulation/

├── data/
├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_variable_diagnostics.ipynb
│   ├── 03_woe_binning_and_iv_selection.ipynb
│   ├── 04_pd_model_logistic.ipynb
│   ├── 05_rho_estimation_vasicek.ipynb
│   ├── 06_lgd_ead_ecl_model.ipynb
│
├── results/
├── src/
├── README.md
├── LICENSE
└── .gitignore
```

---

# 🔎 Step 1 — Data Preparation

* Filtering relevant loan statuses
* Creating binary default variable
* Removing data leakage variables
* Handling missing values
* Winsorizing extreme values (1%–99%)
* Creating missing indicator variables

---

# 📊 Step 2 — Variable Diagnostics

* Distribution and skewness analysis
* Event rate analysis
* Multicollinearity checks

Example:

* `grade` removed due to high correlation with `sub_grade`

---

# 🧮 Step 3 — WoE Binning & IV Selection

* Weight of Evidence (WoE) transformation applied
* Ensures monotonic relationship with default
* Improves interpretability of logistic regression

Variables selected using **Information Value (IV)**

---

# 📈 Step 4 — Probability of Default (PD)

* Logistic Regression (Statsmodels)
* Feature selection using statistical significance
* Model evaluation:

  * AUC ≈ 0.70
  * KS ≈ 0.30

### ⚙ PD Calibration

PD calibrated using **intercept adjustment**, based on:

*Model-Based PD Rating Scale Calibration – Logistic Regression Intercept Optimization*

Ensures alignment between predicted and observed default rates.

---

# 💰 Step 5 — LGD, EAD & ECL Modelling

### LGD Model

* Two-stage approach:

  * Probability of recovery
  * Recovery rate conditional on recovery

### EAD Model

* Estimated using **Credit Conversion Factor (CCF)** regression

### ECL Calculation

```
ECL = PD × LGD × EAD
```

* Computed at **loan level**
* Aggregated to portfolio level for analysis

---

# 🔧 Data Alignment (Critical Fix)

Initially, PD, LGD, and EAD were aligned using row order.

This was corrected using **ID-based merging**, ensuring:

* Accurate loan-level matching
* Robustness to dataset ordering
* Production-grade data integrity

---

# 🧮 Step 6 — Asset Correlation (ρ)

* Default rates aggregated by year
* Gaussian transformation applied
* Vasicek framework used to estimate correlation

**Estimated:**

```
ρ ≈ 0.025
```

Consistent with retail credit portfolios.

---

# 📊 Portfolio Risk Framework

At loan level:

```
Expected Loss = PD × LGD × EAD
```

At portfolio level:

* Aggregated ECL
* Year-on-year loss trends
* Risk component analysis (PD, LGD, EAD)

---

# 📊 Key Outputs

* Loan-level PD, LGD, EAD
* Expected Credit Loss (ECL)
* Variable importance and diagnostics
* Asset correlation (ρ)
* Portfolio-level loss insights

---

# 🧠 Learning Focus

* Credit risk modelling (PD, LGD, EAD)
* WoE & IV techniques
* Logistic regression interpretation
* Portfolio credit risk theory
* Vasicek model implementation
* End-to-end modelling pipeline design

---

# ⚙️ Tech Stack

* Python
* pandas, numpy
* scipy, statsmodels
* scikit-learn
* matplotlib

Focus is on **interpretability and financial logic**, not black-box ML.

---

# 🚀 Future Extensions

* Monte Carlo Vasicek simulation
* Portfolio loss distribution
* Economic capital (99.9 percentile)
* Stress testing scenarios
* Scenario-based credit risk analysis

---

# 📌 Model Assumptions

* Large homogeneous retail portfolio
* Unsecured loans
* No credit risk mitigation
* Single systematic factor (Vasicek)

---

# 📌 Project Status

✔ Data Preparation
✔ Variable Diagnostics
✔ WoE & IV Selection
✔ PD Model + Calibration
✔ LGD Model
✔ EAD Model
✔ ECL Computation
✔ Asset Correlation (ρ)

**Next:** Portfolio Simulation & Economic Capital

---

# 👤 Author

**Amitabh Gogoi**
Credit Risk & Financial Analysis
PD / LGD / EAD | IFRS-9 | Portfolio Risk Analytics

---

# 📌 Summary

This project demonstrates a **complete, interpretable credit risk pipeline**, moving from borrower-level modelling to portfolio-level risk — aligned with real-world banking frameworks.

---
