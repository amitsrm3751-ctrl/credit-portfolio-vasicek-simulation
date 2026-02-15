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

---

## 🧱 Project Structure

credit-portfolio-vasicek-simulation/

│
├── data/
│ └── Lending_Data.csv
│
├── notebooks/
│ ├── 01_data_cleaning.ipynb
│ ├── 02_pd_model.ipynb
│ ├── 03_lgd_estimation.ipynb
│ ├── 04_ead_estimation.ipynb
│ └── 05_vasicek_simulation.ipynb
│
└── README.md

---

## 🔎 Step 1 — Data Cleaning

- Filter relevant loan statuses  
- Define binary default target  
- Remove leakage variables  
- Handle missing values  
- Convert financial columns to numeric  

Focus: clean modelling dataset with no forward-looking bias.

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

LGD calculated for Charged Off loans:

\[
LGD = \frac{Funded Amount - Total Principal Recovered - Recoveries}{Funded Amount}
\]

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

\[
ρ = 0.12 \text{ to } 0.24
\]

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

## 📌 Status

🟡 Project Initialized  
Data cleaning and modelling notebooks under development.

---

## 👤 Author

Amitabh Gogoi  
Credit Analysis and Risk | IFRS-9 | PD / LGD / EAD | Portfolio Risk Analytics  

