# 📊 Credit Portfolio Risk Modelling & Vasicek Simulation

A structured end-to-end credit risk modelling project using real Lending Club loan data.

This project builds a clean and interpretable pipeline covering:

- Probability of Default (PD)
- Loss Given Default (LGD)
- Exposure at Default (EAD)
- Portfolio loss simulation using the Vasicek single-factor model

The goal is to connect retail credit modelling with portfolio-level economic capital estimation.

---

## 🎯 Project Objective

To build a transparent credit risk framework that:

1. Estimates borrower-level PD using Logistic Regression  
2. Computes realized LGD from recovery data  
3. Approximates EAD for installment loans  
4. Simulates portfolio loss distribution using Monte Carlo  
5. Studies the impact of asset correlation (ρ) on Economic Capital  

This bridges individual loan modelling with portfolio credit risk theory.

---

## 📂 Dataset

**Source:** Lending Club loan dataset (public)

The dataset includes:

- Loan amount and term
- Interest rate and installment
- Borrower characteristics
- Loan status (Fully Paid / Charged Off / Current)
- Recovery amounts
- Outstanding principal

For modelling integrity:

- `Charged Off` → Default = 1  
- `Fully Paid` → Default = 0  
- `Current` loans are excluded from PD training  

## 📂 Project Structure

```
credit-portfolio-vasicek-simulation/

│
├── data/
│   └── processed/
│       └── loan_data_cleaned.csv
│
├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_variable_diagnostics.ipynb
│   ├── 03_binning_woe_iv.ipynb
│   ├── 04_pd_model_logistic.ipynb
│   └── 05_vasicek_portfolio_simulation.ipynb
│
└── README.md
```
## 🔎 Step 1 — Data Cleaning

- Filter relevant loan statuses  
- Define binary default target  
- Remove leakage variables  
- Handle missing values  
- Convert financial columns to numeric  

Before building the PD model, variables are examined to understand their statistical properties and relationship with default.

Diagnostics performed include:

- Summary statistics and distribution analysis
- Skewness and kurtosis examination
- Event rate analysis across categorical variables
- Identification of multicollinearity (e.g., grade vs sub_grade)
- Removal of redundant predictors

Focus: understand variable behaviour and ensure predictors are suitable for modelling.

---

## 📈 Step 2 — Probability of Default (PD)

- Train/Test split  
- Logistic Regression baseline  
- Model evaluation:
  - ROC / AUC
  - KS Statistic
  - Gini Coefficient  
- Interpretation of coefficients  

Objective: build an interpretable and statistically sound PD model.

---

## 💰 Step 3 — Loss Given Default (LGD)

LGD (Loss Given Default) is defined as:

LGD = (Exposure at Default − Recoveries) / Exposure at Default

- Distribution analysis
- Average LGD estimation
- Sensitivity across borrower segments

This uses actual recovery data (not proxy severity scores).

---

## 💳 Step 4 — Exposure at Default (EAD)

For installment loans:

- Initial approximation: `EAD ≈ Funded Amount`
- Alternative approximation: `EAD ≈ Outstanding Principal`

Simple and transparent estimation suitable for retail portfolios.

---

## 🧮 Step 5 — Vasicek Portfolio Simulation

Using:

- Estimated portfolio PD
- Average LGD
- Exposure per loan

Monte Carlo simulation is performed under the **Vasicek single-factor model**:

- Simulate systematic risk factor
- Compute conditional default probability
- Generate portfolio loss distribution
- Calculate Value at Risk (VaR)
- Estimate Economic Capital

Asset correlation (ρ) varied from:


ρ = 0.12  to  0.24


to analyze its impact on tail risk and capital requirements.

---

## 📊 Expected Outputs

- Borrower-level PD estimates  
- Realized LGD distribution  
- Portfolio loss distribution  
- Economic Capital under different correlation scenarios  
- Visualization of loss quantiles  

---

## 🧠 Learning Focus

This project is designed to strengthen understanding of:

- Retail credit modelling  
- Recovery-based LGD estimation  
- Portfolio credit risk theory  
- Monte Carlo simulation in Python  
- Relationship between correlation and tail risk  

---

## ⚙️ Tech Stack

- Python  
- pandas  
- numpy  
- scipy  
- scikit-learn  
- matplotlib  

No advanced ML libraries used — focus is on fundamentals.

---

## 🚀 Future Extensions (Optional)

- WOE transformation and scorecard development  
- PD calibration  
- Stress testing scenarios  
- Analytical Vasicek closed-form capital calculation  
- Comparison of simulation vs Basel IRB formula  

---
---

## 📌 Key Assumptions

- Portfolio treated as a large homogeneous retail portfolio for Vasicek simulation.
- Loans treated as unsecured retail exposures.
- No Credit Risk Mitigation (CRM) adjustments applied.
- Asset correlation (ρ) is exogenously specified and varied for sensitivity analysis.
- Maturity adjustment is not incorporated (retail simplification).
- Economic Capital estimated at 99.9% confidence level using Monte Carlo simulation.

---

## 🏛 Regulatory Interpretation

- The Vasicek single-factor framework underpins the Basel IRB capital formula.
- Under the Standardised Approach, credit risk mitigation (CRM) typically reduces Exposure at Default (EAD).
- Under the IRB approach, collateral more commonly affects Loss Given Default (LGD).
- This project focuses on unsecured retail exposures; therefore, CRM-adjusted EAD is not applicable.
- Economic Capital estimated here is model-based and may differ from Regulatory Capital requirements.

---

## ⚠ Model Limitations

- Homogeneous portfolio assumption may understate concentration risk.
- LGD is based on observed recoveries and does not incorporate downturn LGD adjustment.
- Correlation parameter is assumed rather than empirically calibrated.
- Simulation results approximate large portfolio behavior; smaller portfolios may exhibit higher loss variance.

## 📌 Project Status

✔ Data Preparation Completed  
- Missing value treatment with structured approach  
- Outlier capping using 1%–99% percentile winsorization  
- Feature engineering (credit age variables)  
- Missing indicator variables created  
- Clean modelling dataset exported (`loan_data_cleaned.csv`)

✔ Variable Diagnostics Completed  
- Summary statistics and distribution analysis  
- Skewness and kurtosis evaluation  
- Event rate analysis for `grade` and `sub_grade`  
- Multicollinearity identified and handled (`grade` removed)

Next Steps:
- Weight of Evidence (WoE) binning
- Information Value (IV) calculation
- Logistic Regression PD model
- Vasicek portfolio loss simulation

## 👤 Author

Amitabh Gogoi  
Credit Analysis and Risk | IFRS-9 | PD / LGD / EAD | Portfolio Risk Analytics  

