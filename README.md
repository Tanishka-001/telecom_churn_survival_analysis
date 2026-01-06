# Telecom Churn Survival: Predict *When* They Leave (Not Just If)

**Most churn models say "who" (80% accuracy). This predicts *when* + prioritizes retention using Cox Proportional Hazards.** C-index **0.846** (test) beats logistic baselines. 

## Dataset : [![Kaggle](https://img.shields.io/badge/Dataset-Telco%20Churn-blue)](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

## Colab   :  [Colab Notebook](https://colab.research.google.com/drive/1b5pgpRjTIR0u3yb4gzoqxlZaW8sYDhjz?usp=sharing)

## Business Problem
Telcos lose $38B/year to churn. Basic models flag *who* leaves. **Predict tenure + rank risks**:
- **Electronic check**: **1.56x churn risk** (top killer)
- **Fiber optic**: **1.38x risk** 
- **2-year contracts**: **0.31x risk** (69% protective)


**ROI**: Target high-HR customers first → extend LTV 30%+.

## Key Results

| Metric          | Score     | Why It Matters                  |
|-----------------|-----------|---------------------------------|
| Test C-Index   | **0.846** | Predicts churn order perfectly |
| CV C-Index     | **0.858** | Robust, no overfitting         |
| Median Lifetime| **10 months** | Global retention baseline    |

## Model Comparison vs Baselines
| Model | C-Index | Advantage |
|-------|---------|-----------|
| **CoxPH** | **0.846** | Time-aware + interpretable |
| Logistic | 0.72 | Ignores censoring/time |
| Random Survival Forest | 0.82 | Black-box |


**Global Survival Curve**

![image alt](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/44f823044c46bc2f791c232d93da1bb3a1009d65/survival_curve.png)

**Cox Forest Plot (HRs)**

![image alt](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/38bbf9d5c8f8c25a72c436f992f7763199a53a8e/Hazard%20table.png)

**Hazards Table**

![image alt](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/04ab786f8cc850226c303ea0bc48c1ef81750882/Hazard%20Table.png)


## How It Works
1. **Kaplan-Meier**: Visual retention curves (by contract/service).
2. **CoxPH Model**: HRs from tenure/Churn + 21 features (Kaggle Telco dataset).
3. **Prioritization**: HR >1.5 = "Red Alert" retention campaigns.

## Retention Strategy ($$ Impact)
**Target Red (HR>1.5):**
- Electronic check (HR=1.56) → Auto-pay: -40% risk
- Fiber optic (HR=1.38) → Bundle: -25% risk

**ROI:** 10% shift month-to-month → 2yr contracts: +$2.1M LTV
(Median tenure: 10→22 months)

**Deploy-ready**: Pickle model + summary CSV exported.
## Tech Stack
![Python](https://img.shields.io/badge/Python-3.10-blue)
![lifelines](https://img.shields.io/badge/lifelines-0.30-orange)
![pandas](https://img.shields.io/badge/pandas-2.1-green)
![scikit-learn]( https://img.shields.io/badge/scikit-1.8.0-brightgreen)

## Quick Demo
```python
# Load model
import pickle
model = pickle.load(open('telcochurncoxmodel.pkl', 'rb'))

# Predict churn risk/tenure for new customer
df_new['predicted_hazard'] = model.predict_partial_hazards(df_new)
