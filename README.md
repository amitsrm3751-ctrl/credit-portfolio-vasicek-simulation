# 📊 Credit Risk Modelling & Vasicek Framework (Learning Project)

This project builds an end-to-end **credit risk modelling pipeline** using loan-level data, covering:

* Probability of Default (PD)
* Loss Given Default (LGD)
* Exposure at Default (EAD)
* Expected Credit Loss (ECL)
* Basic portfolio risk analysis using the Vasicek framework

The goal is to **understand and implement core credit risk concepts** through a structured, hands-on approach.

---

# 🎯 Project Objective

This project demonstrates how key credit risk components are built and connected:

* Estimate **PD** using Logistic Regression
* Model **LGD** using a two-stage approach
* Estimate **EAD** using a CCF-based regression
* Compute **Expected Loss (ECL = PD × LGD × EAD)**
* Explore **portfolio-level behavior** using a simplified Vasicek model

This is a **learning-focused implementation**, not a production or regulatory model.

---

# 📂 Dataset

**Source:** Lending Club Loan Dataset

Includes:

* Loan characteristics (amount, term, interest rate)
* Borrower attributes
* Loan outcomes (Fully Paid / Charged Off)

### Target Definition

* Charged Off → Default = 1
* Fully Paid → Default = 0

Loans with status *Current* are excluded.

---

# 📂 Project Structure

```id="proj-struct"
credit-portfolio-vasicek-simulation/

├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_variable_diagnostics.ipynb
│   ├── 03_woe_binning_and_iv_selection.ipynb
│   ├── 04_pd_model_logistic.ipynb
│   ├── 05_rho_estimation_vasicek.ipynb
│   ├── 06_lgd_ead_ecl_model.ipynb
│
├── data/
├── README.md
└── .gitignore
```

---

# 🔎 Step 1 — Data Preparation

* Filtering relevant loan statuses
* Creating binary default variable
* Removing leakage variables
* Handling missing values
* Creating missing indicators

---

# 📊 Step 2 — Variable Diagnostics

* Distribution analysis
* Event rate checks
* Basic feature screening

---

# 🧮 Step 3 — WoE Binning & IV

* Applied **Weight of Evidence (WoE)** transformation
* Checked monotonic relationship with default
* Used **Information Value (IV)** for feature selection

---

# 📈 Step 4 — Probability of Default (PD)

* Logistic Regression model
* Features based on WoE-transformed variables

Evaluation:

* AUC ≈ 0.70
* KS ≈ 0.30

---

# 💰 Step 5 — LGD, EAD & ECL

### LGD

* Two-stage modelling:

  * Recovery probability
  * Recovery rate

### EAD

* Estimated using a regression-based approach

### Expected Loss

```id="ecl-eq"
ECL = PD × LGD × EAD
```

Computed at **loan level** and aggregated for analysis.

---

# 🔧 Data Alignment Note

Initially, PD, LGD, and EAD were aligned using row order.

This was corrected by introducing **ID-based matching**, ensuring proper alignment of loan-level predictions across models.

---

# 🧮 Step 6 — Vasicek Correlation (ρ)

* Default rates aggregated by year
* Used to estimate asset correlation (ρ)
* Simple implementation for learning purposes

---

# 📊 Outputs

* Loan-level PD, LGD, EAD
* Expected Loss (ECL)
* Year-wise aggregation of portfolio metrics
* Basic visualization of risk components

---

# 🧠 Learning Focus

* Understanding PD, LGD, EAD modelling
* Feature engineering with WoE
* Logistic regression interpretation
* Linking loan-level models to portfolio view
* Hands-on implementation of risk concepts

---

# ⚙️ Tech Stack

* Python
* pandas, numpy
* scikit-learn, statsmodels
* matplotlib

---

# ⚠️ Disclaimer

This project is created for **learning and exploration purposes only**.

* It is **not a production model**
* It does not follow full regulatory requirements (e.g., Basel, IFRS 9)
* Simplifications have been made for clarity and understanding

---

# 👤 Author

Amitabh Gogoi

---

# 📌 Summary

This project demonstrates how core credit risk components (PD, LGD, EAD) can be built and combined to estimate expected loss, along with a simple portfolio-level extension using the Vasicek framework.

---
