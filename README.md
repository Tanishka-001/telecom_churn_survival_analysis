![Survival Analysis Badge](https://img.shields.io/badge/Survival%20Analysis-CoxPH%20C%2DIndex%200.846-brightgreen)

# Telecom Churn Survival: Predict *When* They Leave (Not Just If)

**Most churn models say "who" (80% accuracy). This predicts *when* + prioritizes retention using Cox Proportional Hazards.** C-index **0.846** (test) beats logistic baselines. [Colab Notebook](https://colab.research.google.com/github/Tanishka-001/telecom-churn-survival-analysis/blob/main/churn_survival_analysis.ipynb)

## Business Problem
Telcos lose $X billion/year to churn. Basic models flag *who* leaves. **We predict tenure + rank risks**:
- Month-to-month: **2.27x churn speed** (HR)
- Fiber optic: **1.38x risk**
- 2-year contracts: **0.69x risk** (protective)

**ROI**: Target high-HR customers first → extend LTV 30%+.

## 📊 Key Results

| Metric          | Score     | Why It Matters                  |
|-----------------|-----------|---------------------------------|
| Test C-Index   | **0.846** | Predicts churn order perfectly |
| CV C-Index     | **0.858** | Robust, no overfitting         |
| Median Lifetime| **10 months** | Global retention baseline    |

**Global Survival Curve** ![image alt](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/44f823044c46bc2f791c232d93da1bb3a1009d65/survival_curve.png)

![Cox Forest Plot (HRs)](cox_forest.png)
![Hazards Table](cox_hazards.png)

## 🛠️ How It Works
1. **Kaplan-Meier**: Visual retention curves (by contract/service).
2. **CoxPH Model**: HRs from tenure/Churn + 21 features (Kaggle Telco dataset).
3. **Prioritization**: HR >1.5 = "Red Alert" retention campaigns.

**Deploy-ready**: Pickle model + summary CSV exported.

## 🚀 Quick Demo
```python
# Load model
import pickle
model = pickle.load(open('telcochurncoxmodel.pkl', 'rb'))

# Predict churn risk/tenure for new customer
df_new['predicted_hazard'] = model.predict_partial_hazards(df_new)
