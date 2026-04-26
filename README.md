# Credit Risk Modelling & Portfolio Simulation (Vasicek + Bayesian Extension)

This project builds an end-to-end credit risk modelling pipeline, extending from loan-level estimation to portfolio-level loss simulation and Bayesian uncertainty modelling.

It combines classical credit risk modelling (PD, LGD, EAD) with:

- Monte Carlo simulation  
- Vasicek single-factor credit risk framework  
- Bayesian inference for PD uncertainty  

---

## 🎯 Project Overview

The project is structured in three layers:

### 1. Loan-Level Models
- Probability of Default (PD) using Logistic Regression  
- Loss Given Default (LGD) using a two-stage model  
- Exposure at Default (EAD) using CCF-based regression  
- Expected Credit Loss (ECL = PD × LGD × EAD)

---

### 2. Portfolio-Level Risk
- Correlated defaults via Vasicek framework  
- Monte Carlo simulation of loss distribution  
- Risk metrics:
  - Expected Loss (EL)
  - Value-at-Risk (VaR 99.9%)
  - Conditional VaR (CVaR)
  - Economic Capital  

---

### 3. Bayesian Extension
- PD modeled as a distribution (Beta-Binomial), not a point estimate  
- Captures parameter uncertainty  
- Enables data-driven stress scenarios  

---

## 🧠 Core Insight

Credit risk is not driven by individual defaults,  
but by how defaults **cluster under economic stress** —  
and how uncertain we are about those probabilities.

---

## 📂 Dataset

**Source:** Lending Club Loan Dataset  

**Target Definition:**
- Charged Off → Default = 1  
- Fully Paid → Default = 0  
- Current loans excluded  


---

## 📂 Project Structure

```
credit-portfolio-vasicek-simulation/

├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_variable_diagnostics.ipynb
│   ├── 03_woe_binning_and_iv_selection.ipynb
│   ├── 04_pd_model_logistic.ipynb
│   ├── 05_rho_estimation_vasicek.ipynb
│   ├── 06_lgd_ead_ecl_model.ipynb
│   ├── 07_vasicek_monte_carlo.ipynb
│   ├── 08_bayesian_pd_beta_binomial.ipynb
│   ├── 09_bayesian_stress_testing.ipynb
│
├── data/
├── README.md
└── .gitignore
```

---


---

## 🔎 Methodology

### 1. Data Preparation
- Filtering relevant loan statuses  
- Creating binary default variable  
- Handling missing values  
- Removing leakage variables  

---

### 2. Variable Diagnostics
- Distribution analysis  
- Event rate checks  
- Feature screening  

---

### 3. WoE Binning & IV
- Weight of Evidence (WoE) transformation  
- Monotonic binning  
- Information Value (IV) for feature selection  

---

### 4. Probability of Default (PD)
- Logistic Regression with WoE features  

**Performance:**
- AUC ≈ 0.70  
- KS ≈ 0.30  

---

### 5. LGD, EAD & ECL

**LGD:**
- Two-stage model:
  - Recovery probability  
  - Recovery rate  

**EAD:**
- Regression-based Credit Conversion Factor (CCF)  

**Expected Loss:**
\[
ECL = PD \times LGD \times EAD
\]

---

### 6. Vasicek Correlation (ρ)
- Estimated from historical default rates  
- Captures systematic dependence across borrowers  

---

### 7. Monte Carlo Portfolio Simulation

Z ~ N(0, 1)

PD(Z) = Φ((Φ⁻¹(PD) - √ρ · Z) / √(1 - ρ))

- Simulates correlated defaults  
- Generates full loss distribution  

**Outputs:**
- Expected Loss (EL)  
- VaR (99.9%)  
- CVaR  
- Economic Capital  

---

## ⚡ Computational Design

- Batch vectorized simulation  
- Avoided full matrix allocation (~18GB memory)  
- Balanced performance and memory efficiency  

---

## 🧮 Bayesian Extension (Notebook 08 & 09)

### Problem
Traditional models treat PD as a fixed number, ignoring estimation uncertainty.

---

### Solution: Beta-Binomial Model

**Prior:**  
PD ~ Beta(α, β)

**Posterior:**  
PD | data ~ Beta(α + D, β + n − D)

**Posterior Mean:**  
E[PD] = (α + D) / (α + β + n)
---

### Key Concepts
- PD becomes a distribution  
- Uncertainty explicitly modeled  
- Small samples → wide uncertainty  
- Large samples → convergence  

---

### Bayesian Stress Testing

Instead of arbitrary stress assumptions:

- 5th percentile → optimistic  
- Mean → baseline  
- 95th percentile → stressed  

Each scenario is propagated through the full Monte Carlo simulation.

---

## 📊 Key Results

- Simulated EL closely matches model ECL (validation)  
- Loss distribution:
  - Right-skewed  
  - Fat-tailed  
- Economic Capital ≈ **13% of exposure**  
- Strong dependence on systematic factor (R² ≈ 0.99)  

---

## 🔬 Model Validation

- Compared Monte Carlo results with closed-form Vasicek VaR  
- Differences explained by:
  - Homogeneous vs heterogeneous assumptions  

---

## 📊 Correlation Sensitivity

- Higher ρ ⇒ higher VaR and Economic Capital  
- Demonstrates default clustering effect  

---

## 🧠 Learning Outcomes

- End-to-end credit risk modelling  
- Portfolio loss simulation  
- Systematic vs idiosyncratic risk  
- Efficient Monte Carlo implementation  
- Bayesian inference in credit risk  
- Parameter uncertainty and stress testing  

---

## ⚙️ Tech Stack

- Python  
- pandas, numpy  
- scikit-learn, statsmodels  
- scipy  
- matplotlib  

---

## ⚠️ Disclaimer

- Learning project  
- Not a production/regulatory model  
- Simplifications applied (single-factor, static PD, etc.)  

---

## 👤 Author

**Amitabh Gogoi**

---

## 📌 Final Thought

In credit risk, diversification removes noise —  
but not the storm.

And sometimes, the uncertainty in the model  
matters as much as the risk it predicts.
