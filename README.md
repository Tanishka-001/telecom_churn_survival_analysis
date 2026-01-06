# Telecom Churn Survival Analysis: CoxPH Lifetime Prediction (C-index 0.846)

## Executive Summary

### Business Problem
Telcos lose **$38B/year** to churn. Traditional models predict *who* leaves (~80% acc) but ignore *when* and censoring, missing retention timing.

### Business Solution
Kaplan-Meier curves + Cox Proportional Hazards (CoxPH) on 7,043 Kaggle Telco customers—forecasts tenure/ranks risks via hazard ratios.

### Number Impact
- Electronic check: **1.56x risk** → auto-pay **-40% risk**
- Fiber optic: **1.38x risk** → bundles **-25% churn**  
- 2-yr contracts: **0.31x risk** → **+$2.1M LTV** (10% shift)

[Colab Notebook](https://colab.research.google.com/drive/1b5pgpRjTIR0u3yb4gzoqxlZaW8sYDhjz?usp=sharing)

## Business Problem Pic

![Survival Curve](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/44f823044c46bc2f791c232d93da1bb3a1009d65/survival_curve.png)
*Month-to-month plummets 50% Month 8; 2-yr >90% retention—timing gap binary models miss.*


![KM Curves](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/38bbf9d5c8f8c25a72c436f992f7763199a53a8e/Hazard%20table.png)
*Electronic check (top red): fastest churn risk—urgent retention target.*

## Methodology 
1. Data: Kaggle Telco-Churn (21 feats)
2. Prep: Nulls→median, encode, tenure 0→0.5mo
3. Kaplan-Meier: Stratified curves by contract/service
4. CoxPH: lifelines.CoxPHFitter → HRs + hazards. CV 0.858

## Skills Used 
![Python](https://img.shields.io/badge/Python-3.10-blue) ![pandas](https://img.shields.io/badge/pandas-2.1-green) ![lifelines](https://img.shields.io/badge/lifelines-0.30-orange) ![scikit-learn]( https://img.shields.io/badge/scikit-1.8.0-brightgreen)

Python | pandas | lifelines | matplotlib | Survival Analysis | EDA | scikit-learn

## Results
**C-index**: 0.846 test / 0.858 CV | Median survival: 10 months

| Top HR Risks | Value |
|--------------|-------|
| Electronic check | 1.56x |
| Fiber optic | 1.38x |
| No phone | 1.24x |

![Hazards](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/04ab786f8cc850226c303ea0bc48c1ef81750882/Hazard%20Table.png)

### Business Recommendation
1. **HR>1.5**: Electronic → auto-pay (-40%)
2. **Fiber**: Bundles (-25%)  
3. **Upsell**: Month-to-month → 2-yr (+5x LTV)
**ROI**: **$2.1M** from 10% conversion

## Next Steps that could be done
**Different Steps**: Weibull/RSF models; time-varying covariates

**Outside Scope**: A/B sims; RFM+survival; Streamlit app; MLflow pipeline

**Limitations**: Monthly data → daily; add usage feats; multi-dataset validation

---

**Demo**:
```python
import pickle; import pandas as pd
model = pickle.load(open('telcochurncoxmodel.pkl', 'rb'))
df_new = pd.read_csv('new_customers.csv')
df_new['hazard'] = model.predict_partial_hazards(df_new)
print(df_new[['CustomerID', 'hazard']].sort_values('hazard', ascending=False))


