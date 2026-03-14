# 📊 Credit Portfolio Risk Modelling & Vasicek Framework

A structured end-to-end **credit risk modelling project** using the public **Lending Club loan dataset**.

This project builds a transparent and interpretable modelling pipeline covering:

* Probability of Default (**PD**)
* Asset correlation estimation (**ρ**) using the **Vasicek framework**
* Future extensions for **Loss Given Default (LGD)** and **Exposure at Default (EAD)**
* Portfolio loss modelling and **economic capital estimation**

The objective is to connect **borrower-level credit modelling** with **portfolio-level credit risk analysis**.

---

# 🎯 Project Objective

This project builds a simplified but realistic **credit risk modelling framework** that:

1. Estimates borrower-level **Probability of Default (PD)** using Logistic Regression
2. Applies **Weight of Evidence (WoE)** binning and **Information Value (IV)** for variable selection
3. Calibrates PD estimates using **intercept adjustment**
4. Estimates **asset correlation (ρ)** using the **Vasicek single-factor model**
5. Provides a foundation for **portfolio credit risk simulation**

The project bridges **retail credit modelling techniques** with **portfolio credit risk theory** used in regulatory frameworks such as **Basel IRB**.

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

Target definition used for PD modelling:

```
Charged Off  → Default = 1
Fully Paid   → Default = 0
```

Loans with status **Current** are excluded from model training.

⚠ **Note:**
Due to GitHub file size limits, the raw dataset is **not included in this repository**.

---

# 📂 Project Structure

```
credit-risk-modelling/

├── data/
│
├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_variable_diagnostics.ipynb
│   ├── 03_woe_binning_and_iv_selection.ipynb
│   ├── 04_pd_model_logistic.ipynb
│   ├── 05_rho_estimation_vasicek.ipynb
│
├── results/
├── src/
│
├── README.md
├── LICENSE
└── .gitignore
```

The workflow is organized as **sequential modelling notebooks** so the modelling pipeline can be followed step-by-step.

---

# 🔎 Step 1 — Data Preparation

Key preprocessing steps include:

* Filtering relevant loan statuses
* Creating the binary **default indicator**
* Removing potential **data leakage variables**
* Handling missing values
* Converting financial variables to numeric format
* Winsorizing extreme values (1% – 99%)
* Creating missing indicator variables

The output is a **clean modelling dataset** for credit risk analysis.

---

# 📊 Step 2 — Variable Diagnostics

Exploratory analysis is performed to understand predictor behaviour:

* Summary statistics
* Distribution analysis
* Skewness and kurtosis examination
* Event rate analysis across categorical variables
* Multicollinearity inspection

Example:

```
grade vs sub_grade → high correlation
```

To avoid redundancy, **grade is removed from the model**.

---

# 🧮 Step 3 — WoE Binning & Information Value

Predictor variables are transformed using **Weight of Evidence (WoE)** binning.

Advantages of WoE transformation:

* Creates **monotonic relationships with default**
* Improves **interpretability of logistic regression coefficients**
* Aligns with traditional **credit scorecard modelling**

Predictive strength of variables is evaluated using **Information Value (IV)**.

---

# 📈 Step 4 — Probability of Default (PD) Model

The PD model is estimated using **Logistic Regression (Statsmodels)**.

Steps include:

* Train / Test split
* Logistic regression estimation
* Statistical significance testing (p-values)
* Feature selection based on model diagnostics

Model performance metrics include:

* ROC Curve
* **AUC ≈ 0.70**
* KS Statistic ≈ **0.30**
* Gini coefficient

The objective is to produce a **transparent and interpretable credit risk model**.

---

# ⚙ PD Calibration

After estimation, the PD model is calibrated using **logistic regression intercept adjustment**.

This follows the concept described in the paper:

**“Model-Based PD Rating Scale Calibration – Logistic Regression Intercept Optimization”**

Calibration aligns the **average predicted PD** with the **observed portfolio default rate**, ensuring consistency between model predictions and empirical default frequency.

---

# 🧮 Asset Correlation Estimation (ρ)

To incorporate portfolio credit risk dependence, the project estimates the **asset correlation parameter (ρ)** using the **Vasicek single-factor framework**.

Steps:

1. Aggregate **observed default rates by year**
2. Transform default rates using the **inverse normal transformation**
3. Estimate the **variance of the systematic factor**

The estimated asset correlation is approximately:

```
ρ ≈ 0.025
```

This value is consistent with typical **retail credit portfolio correlations**.

---

# 💰 Portfolio Risk Framework

In portfolio credit risk modelling:

```
Expected Loss = PD × LGD × EAD
```

Where:

* **PD** = Probability of Default
* **LGD** = Loss Given Default
* **EAD** = Exposure at Default

This project currently estimates:

* **PD**
* **Asset correlation (ρ)**

Future extensions will include modelling of **LGD and EAD**, enabling full **portfolio loss simulation**.

---

# 📊 Expected Outputs

* Borrower-level **PD estimates**
* Variable predictive strength analysis
* Asset correlation estimation
* Portfolio credit risk parameters for simulation

---

# 🧠 Learning Focus

This project reinforces concepts in:

* Retail credit risk modelling
* Logistic regression PD models
* WoE binning and IV analysis
* Portfolio credit risk theory
* Vasicek asset correlation estimation
* Credit risk modelling pipelines

---

# ⚙️ Tech Stack

* Python
* pandas
* numpy
* scipy
* statsmodels
* scikit-learn
* matplotlib

The project intentionally emphasizes **interpretable statistical modelling** rather than complex machine learning approaches.

---

# 🚀 Future Extensions

Planned additions include:

* **LGD modelling**
* **EAD estimation**
* **Monte Carlo Vasicek portfolio simulation**
* Portfolio **loss distribution**
* **Economic capital estimation**
* Stress testing scenarios

---

# 📌 Model Assumptions

* Portfolio treated as a **large homogeneous retail portfolio**
* Loans treated as **unsecured exposures**
* No credit risk mitigation applied
* Correlation captured through the **Vasicek systematic factor**

---

# 📌 Project Status

✔ Data Preparation Completed
✔ Variable Diagnostics Completed
✔ WoE Binning & IV Analysis Completed
✔ Logistic Regression PD Model
✔ PD Calibration
✔ Asset Correlation Estimation (ρ)

Next Steps:

* LGD modelling
* EAD estimation
* Portfolio loss simulation
* Economic capital estimation

---

# 👤 Author

**Amitabh Gogoi**

Credit Risk & Financial Analysis
IFRS-9 | PD / LGD / EAD | Portfolio Risk Analytics
