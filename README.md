# Causal Inference Using IPW & AIPW with Machine Learning Models

This project conducts a comparative analysis of **Inverse Probability Weighting (IPW)** and **Augmented Inverse Probability Weighting (AIPW)** methods for causal inference using synthetic observational data. The work is backed by a thorough implementation of machine learning models to estimate treatment effects, validate robustness, and explore estimator efficiency.

> 🎓 Developed as part of a graduate-level coursework submission at Université Côte d’Azur.

---

## 🧠 Project Overview

The project explores **causal inference** in healthcare-like settings where **randomized controlled trials (RCTs)** are often impractical. Using a synthetically generated dataset of 5000 samples, it evaluates the robustness and efficiency of:

- IPW — a basic propensity score weighting approach
- AIPW — a doubly robust estimator that combines propensity scores and outcome regression

### 🛠 Key Techniques

- **Propensity Score Estimation** (Logistic Regression)
- **Outcome Models**: Linear Regression, Random Forest, Gradient Boosting
- **Frameworks Used**: `DoWhy`, `EconML`, and `CausalML`
- **Robustness Checks**: Placebo tests, data subset refuters, and random confounders

---

## 🧪 Dataset Description

Synthetic data simulates real-world healthcare variables:

| Feature | Type | Description |
|--------|------|-------------|
| Age | Continuous | Patient age |
| Sex | Binary | 0 = Female, 1 = Male |
| Heart Rate | Continuous | Baseline heart rate |
| Blood Pressure | Continuous | Systolic BP |
| Comorbidity Index | Categorical | 0 = Low, 1 = Moderate, 2 = High |
| Lifestyle Factors | Binary | 0 = Healthy, 1 = Unhealthy |
| Treatment | Binary | Drug administered (0 = No, 1 = Yes) |
| Outcome | Continuous | Proarrhythmic Risk |

---

## 📈 Results Summary

| Method | ATE Estimate | Notes |
|--------|--------------|-------|
| **IPW** | 0.5316 | Higher sensitivity to extreme weights |
| **AIPW (DoWhy)** | 0.4879 | More stable and efficient |
| **AIPW (Manual)** | ~0.49 | Matches DoWhy closely |
| **AIPW (CausalML)** | ~0.44 | Captures non-linearity well |
| **AIPW (EconML)** | ~0.47 | Consistent with DoWhy |

> ✅ AIPW consistently provided **lower variance and more reliable estimates**.



