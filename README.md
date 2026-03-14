# 📊 Credit Portfolio Risk Modelling & Vasicek Simulation

A structured end-to-end **credit risk modelling project** using the public **Lending Club loan dataset**.

This project builds a transparent and interpretable modelling pipeline covering:

* Probability of Default (**PD**)
* Loss Given Default (**LGD**)
* Exposure at Default (**EAD**)
* Portfolio loss simulation using the **Vasicek single-factor model**

The objective is to connect **borrower-level credit modelling** with **portfolio-level economic capital estimation**.

---

# 🎯 Project Objective

This project builds a simplified but realistic credit risk framework that:

1. Estimates borrower-level **Probability of Default (PD)** using Logistic Regression
2. Computes realized **Loss Given Default (LGD)** using recovery data
3. Approximates **Exposure at Default (EAD)** for installment loans
4. Simulates portfolio loss distribution using **Monte Carlo simulation**
5. Studies the impact of **asset correlation (ρ)** on Economic Capital

The project bridges **retail credit modelling** with **portfolio credit risk theory** used in regulatory frameworks such as **Basel IRB**.

---

# 📂 Dataset

**Source:** Public Lending Club Loan Dataset

The dataset includes:

* Loan amount and term
* Interest rate and installment
* Borrower characteristics
* Loan status (Fully Paid / Charged Off / Current)
* Recovery amounts
* Outstanding principal

Target definition:

```
Charged Off  → Default = 1
Fully Paid   → Default = 0
```

Loans with status **Current** are excluded from PD model training.

⚠ **Note:**
Due to GitHub file size limits, the raw dataset is **not included in this repository**.

---

# 📂 Project Structure

```
credit-portfolio-vasicek-simulation/

├── data/
│
├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_variable_diagnostics.ipynb
│   ├── 03_woe_binning_and_iv_selection.ipynb
│   ├── 04_pd_model_logistic.ipynb
│   └── 05_vasicek_portfolio_simulation.ipynb
│
├── results/
├── src/
│
├── README.md
├── LICENSE
└── .gitignore
```

The workflow is organized as **sequential modelling notebooks** to make the pipeline easy to follow.

---

# 🔎 Step 1 — Data Preparation

Key preprocessing steps:

* Filtering relevant loan statuses
* Creating binary default variable
* Removing leakage variables
* Handling missing values
* Converting financial variables to numeric format
* Winsorizing extreme values (1% – 99%)
* Creating missing indicator variables

A clean modelling dataset is produced for downstream analysis.

---

# 📊 Step 2 — Variable Diagnostics

Exploratory analysis is performed to understand predictor behaviour:

* Summary statistics
* Distribution analysis
* Skewness and kurtosis examination
* Event rate analysis across categorical variables
* Multicollinearity identification

Example:

```
grade vs sub_grade → high correlation
```

To avoid redundancy, **grade is removed** from the model.

---

# 🧮 Step 3 — WoE Binning & Information Value

Predictors are transformed using **Weight of Evidence (WoE)**.

This allows:

* Monotonic relationship with default
* Improved logistic regression interpretability
* Consistent scorecard modelling structure

Information Value (IV) is used to evaluate **predictive strength of variables**.

---

# 📈 Step 4 — Probability of Default (PD)

The PD model uses **Logistic Regression**.

Steps include:

* Train / Test split
* Model estimation
* Statistical significance checks (p-values)
* Feature selection

Model evaluation metrics:

* ROC Curve
* AUC
* KS Statistic
* Gini Coefficient

The goal is to produce a **transparent and interpretable credit risk model**.

---

# 💰 Step 5 — Loss Given Default (LGD)

LGD is computed using observed recoveries.

```
LGD = (Exposure at Default − Recoveries) / Exposure at Default
```

Analysis includes:

* LGD distribution
* Average loss severity
* Borrower segment sensitivity

---

# 💳 Step 6 — Exposure at Default (EAD)

For installment loans:

```
EAD ≈ Funded Amount
```

Alternative approximation:

```
EAD ≈ Outstanding Principal
```

This simplification is reasonable for unsecured retail exposures.

---

# 🧮 Step 7 — Vasicek Portfolio Simulation

Portfolio loss distribution is simulated using the **Vasicek single-factor model**.

Monte Carlo simulation steps:

1. Simulate systematic risk factor
2. Compute conditional default probabilities
3. Generate default events
4. Calculate portfolio loss
5. Estimate tail risk

Key outputs:

* Loss distribution
* Value at Risk (VaR)
* Economic Capital

Asset correlation parameter tested across:

```
ρ = 0.12 – 0.24
```

---

# 📊 Expected Outputs

* Borrower-level PD estimates
* LGD distribution
* Portfolio loss distribution
* Economic Capital estimates
* Loss quantile visualization

---

# 🧠 Learning Focus

This project reinforces concepts in:

* Retail credit risk modelling
* Logistic regression PD models
* Recovery-based LGD estimation
* Portfolio credit risk theory
* Monte Carlo simulation
* Correlation effects in credit portfolios

---

# ⚙️ Tech Stack

* Python
* pandas
* numpy
* scipy
* scikit-learn
* matplotlib

The project intentionally avoids complex ML frameworks to emphasize **risk modelling fundamentals**.

---

# 🚀 Future Extensions

Possible extensions include:

* Credit scorecard development
* PD calibration
* Stress testing scenarios
* Analytical Vasicek capital formula
* Comparison with Basel IRB capital requirements

---

# 📌 Key Assumptions

* Portfolio treated as a **large homogeneous retail portfolio**
* Loans treated as **unsecured exposures**
* No credit risk mitigation applied
* Correlation parameter assumed exogenously
* Economic Capital estimated at **99.9% confidence level**

---

# ⚠ Model Limitations

* Homogeneous portfolio assumption ignores concentration risk
* LGD does not incorporate downturn adjustment
* Correlation parameter not empirically calibrated
* Simulation approximates large portfolio behaviour

---

# 📌 Project Status

✔ Data Preparation Completed
✔ Variable Diagnostics Completed
✔ WoE Binning & IV Analysis Completed

Next Steps:

* Logistic Regression PD Model
* LGD estimation
* Vasicek portfolio simulation

---

# 👤 Author

**Amitabh Gogoi**

Credit Analysis and Risk
IFRS-9 | PD / LGD / EAD | Portfolio Risk Analytics
