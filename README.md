# 🧬 Causal Inference Using IPW & AIPW with Machine Learning Models

This project conducts a comparative analysis of **Inverse Probability Weighting (IPW)** and **Augmented Inverse Probability Weighting (AIPW)** for causal inference using synthetic observational data. We explore estimator efficiency, robustness, and sensitivity using multiple machine learning models.

> 🎓 Developed as part of a graduate-level coursework submission at **Université Côte d’Azur**  
> 🧑‍💻 Author: Habeeb Olawale HAMMED
> Supervisors--Safaa Al-Ali:safaa.al-ali@inria.fr, Irene Balelli:irene.baleli@inria. fr

---

## 🧠 Project Overview

In real-world healthcare settings, randomized controlled trials (RCTs) aren't always feasible. This project simulates such a scenario using a **synthetic dataset of 5,000 units** to evaluate two causal inference methods:

- **IPW** — Basic propensity score weighting
- **AIPW** — Doubly robust estimator combining propensity scores and outcome regression

We assess:
- Accuracy and consistency of causal effect estimates
- Performance across different outcome models
- Stability under robustness checks
- Covariate-level contributions to treatment effects

---

## 🛠 Key Techniques & Tools

| Component                  | Details                                                                 |
|---------------------------|-------------------------------------------------------------------------|
| **Propensity Score Model** | Logistic Regression                                                     |
| **Outcome Models**         | Linear Regression, Random Forest, Gradient Boosting                    |
| **Frameworks Used**        | [DoWhy](https://github.com/py-why/dowhy), [EconML](https://github.com/microsoft/EconML), [CausalML](https://github.com/uber/causalml) |
| **Robustness Checks**      | Placebo Test, Data Subset Refuter, Random Confounder                   |
| **Causal DAG**             | Used to define assumptions and backdoor adjustment sets                |

---

## 🧪 Dataset Description

Synthetic data mimics healthcare variables relevant to treatment decisions and outcomes.

| Feature              | Type        | Description                        |
|---------------------|-------------|------------------------------------|
| Age                 | Continuous  | Patient age                        |
| Sex                 | Binary      | 0 = Female, 1 = Male               |
| Heart Rate          | Continuous  | Baseline heart rate                |
| Blood Pressure      | Continuous  | Systolic blood pressure            |
| Comorbidity Index   | Categorical | 0 = Low, 1 = Moderate, 2 = High    |
| Lifestyle Factors   | Binary      | 0 = Healthy, 1 = Unhealthy         |
| Treatment           | Binary      | Drug administered (0 = No, 1 = Yes)|
| Outcome             | Continuous  | Proarrhythmic Risk                 |

---

## 📈 Causal Effect Results Summary

| Method               | ATE Estimate | Notes                                                        |
|----------------------|--------------|--------------------------------------------------------------|
| IPW (DoWhy)          | 0.5316       | High sensitivity to extreme weights                         |
| AIPW (DoWhy)         | 0.4879       | More stable and efficient                                   |
| AIPW (Manual Impl.)  | ~0.49        | Matches DoWhy closely                                       |
| AIPW (CausalML)      | ~0.44        | Captures non-linearity well                                 |
| AIPW (EconML)        | ~0.47        | Consistent with DoWhy, assumes linear outcome model         |

✅ AIPW consistently outperformed IPW by reducing variance and showing resilience to model misspecification.

---

## 🧪 Robustness Checks – Causal Validity

| Test                        | Outcome                                          | Interpretation                                        |
|----------------------------|--------------------------------------------------|--------------------------------------------------------|
| **Placebo Test**           | AIPW drops from 0.4879 → ~0.0105 (p = 0.8)       | Detects no effect under fake treatment — as expected   |
| **Subset Refuter**         | AIPW drops slightly to 0.4264 (p = 0.3)          | Effect is stable even with smaller sample size         |
| **Random Confounder**      | No change in AIPW                                | Irrelevant variables don’t distort the estimate        |

✅ These checks confirm that the causal estimates are **not artifacts of data quirks**, and **AIPW passes all sanity tests**.

---

## 🧬 Covariate-Level Causal Sensitivity Analysis

We tested how **individual covariates** influence the treatment effect using both IPW and AIPW. The AIPW method remained stable, while IPW showed significant inconsistency with multicollinearity.

| Covariate              | IPW ATE      | AIPW ATE     |
|------------------------|--------------|--------------|
| Age                    | ~0.32        | ~0.31        |
| Sex                    | ~0.26        | ~0.25        |
| Heart Rate             | ~0.28        | ~0.27        |
| Blood Pressure         | ~0.33        | ~0.30        |
| Comorbidity Index      | ~0.35        | ~0.34        |
| Lifestyle Factors      | ~0.37        | ~0.36        |
| **All Covariates**     | **-1.065**   | **0.841**    |

- ⚠️ **IPW failed** when using all covariates together — large negative ATE suggests instability.
- ✅ **AIPW stayed consistent** and gave a robust estimate with all variables included.

---

## 🔍 Effect of Outcome Model on AIPW

Different outcome models impact AIPW’s precision:

| Outcome Model       | AIPW ATE Estimate | Notes                                     |
|---------------------|-------------------|-------------------------------------------|
| Linear Regression    | 0.4837            | Overestimates slightly; assumes linearity |
| Random Forest        | 0.4416            | Most conservative; handles non-linearity  |
| Gradient Boosting    | 0.4701            | Balanced performance                      |

➡️ **Random Forest** delivered the most conservative (and likely accurate) estimates, while **Linear Regression** produced inflated results due to its simplicity.

---

## 🧰 How to Run the Code

### 1. Clone the repo
```bash
git clone https://github.com/Haryanfe777/causal-inference-ipw-aipw.git
cd causal-inference-ipw-aipw
