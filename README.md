# Credit Risk Modelling & Portfolio Simulation using Vasicek Framework

This project builds an **end-to-end credit risk modelling pipeline**, extending from loan-level risk estimation to portfolio-level loss simulation and **Bayesian uncertainty modelling**.

It combines **classical credit risk modelling (PD, LGD, EAD)** with:
- **Monte Carlo simulation**
- **Vasicek single-factor framework**
- **Bayesian inference for PD uncertainty**

---

## 🎯 Project Overview

This project demonstrates how modern credit risk systems are built in layers:

### Loan-Level Models
- Estimate **Probability of Default (PD)** using Logistic Regression
- Model **Loss Given Default (LGD)** using a two-stage approach
- Estimate **Exposure at Default (EAD)** using CCF-based regression
- Compute **Expected Credit Loss (ECL)**

### Portfolio-Level Risk
- Model correlated defaults using **Vasicek framework**
- Simulate loss distribution using **Monte Carlo**
- Compute **Economic Capital (VaR, CVaR)**

### Bayesian Extension
- Model PD as a **distribution, not a point estimate**
- Capture **parameter uncertainty**
- Derive **data-driven stress scenarios**

---

## 🧠 Core Insight

> Credit risk is not driven by individual defaults,  
> but by how defaults **cluster under economic stress** —  
> and how uncertain we are about those probabilities.

---

## 📂 Dataset

- Source: Lending Club Loan Dataset

### Target Definition
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

## 🔎 Methodology

### 1. Data Preparation
- Filtering loan statuses
- Creating binary default variable
- Handling missing values
- Removing leakage variables

---

### 2. Variable Diagnostics
- Distribution analysis
- Event rate analysis
- Feature screening

---

### 3. WoE Binning & IV Selection
- Weight of Evidence (WoE) transformation
- Monotonic binning
- Information Value (IV) for feature selection

---

### 4. Probability of Default (PD)
- Logistic Regression model
- WoE-transformed features
- Performance:
  - AUC ≈ 0.70  
  - KS ≈ 0.30  

---

### 5. LGD, EAD & ECL

#### LGD
- Two-stage modelling:
  - Recovery probability
  - Recovery rate

#### EAD
- Regression-based Credit Conversion Factor (CCF)

#### Expected Loss
$$
ECL = PD \times LGD \times EAD
$$

---

### 6. Vasicek Correlation (ρ)
- Estimated from historical default rates
- Captures **systematic dependence across borrowers**

---

### 7. Monte Carlo Portfolio Simulation

#### Framework:
$$
Z \sim \mathcal{N}(0,1)
$$

$$
PD(Z) = \Phi\left(\frac{\Phi^{-1}(PD) - \sqrt{\rho} Z}{\sqrt{1-\rho}}\right)
$$

- Simulate correlated defaults
- Generate portfolio loss distribution
- Compute:
  - Expected Loss (EL)
  - VaR (99.9%)
  - CVaR
  - Economic Capital

---

### ⚡ Computational Design

- Implemented **batch vectorized simulation**
- Avoided full matrix allocation (~18GB memory requirement)
- Balanced **speed vs memory efficiency**

---

## 🧮 Bayesian Extension (Notebook 08 & 09)

### Problem

Traditional models treat PD as a **fixed number**, ignoring estimation uncertainty.

---

### Solution: Beta-Binomial Model

#### Prior:
$$
PD \sim \text{Beta}(\alpha, \beta)
$$

#### Posterior:
$$
PD | data \sim \text{Beta}(\alpha + D, \beta + n - D)
$$

#### Posterior Mean:
$$
\mathbb{E}[PD] = \frac{\alpha + D}{\alpha + \beta + n}
$$

---

### Key Concepts

- PD becomes a **distribution**, not a point estimate  
- Uncertainty is explicitly modeled  
- Small samples → wide uncertainty  
- Large samples → convergence to frequentist estimate  

---

### Bayesian Stress Testing

Instead of arbitrary stress assumptions:

- Use **posterior percentiles**:
  - 5th percentile → optimistic scenario  
  - Mean → base case  
  - 95th percentile → stress scenario  

Each scenario is fed into the **full Monte Carlo simulation**.

---

### Key Insight

> Stress scenarios are derived from **data uncertainty**,  
> not arbitrary assumptions.

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

- Compared Monte Carlo results with **closed-form Vasicek VaR**
- Differences explained by:
  - Homogeneous vs heterogeneous assumptions

---

## 📊 Correlation Sensitivity

- Higher ρ ⇒ higher VaR and Economic Capital  
- Demonstrates **default clustering effect**

---

## 🧠 Learning Outcomes

- End-to-end credit risk modelling
- Portfolio loss simulation
- Systematic vs idiosyncratic risk
- Monte Carlo implementation under constraints
- Bayesian inference in risk modelling
- Parameter uncertainty and stress testing

---

## ⚙️ Tech Stack

- Python
- pandas, numpy
- scikit-learn, statsmodels
- scipy
- matplotlib, seaborn

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

> In credit risk, diversification removes noise —  
> but not the storm.  

> And sometimes, the uncertainty in the model  
> matters as much as the risk it predicts.
