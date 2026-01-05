# Telecom Churn Survival Analysis 

Predicts **churn timing** (C-index **0.846**). Fiber + e-check = danger zone.

## Results
| Metric       | Score  |
|--------------|--------|
| **Test C-Index** | **0.846** |
| **CV C-Index**   | **0.858**  |

**![Survival Curve](survival_curve.png)**
**![Cox Hazards](cox_hazards.png)**

## Insights
- **Risk:** Fiber Optic (HR **1.38**), Electronic Check (**1.56**)
- **Safe:** TechSupport (**0.65**), 2yr Contract (**0.31**)

## Setup
```bash
pip install -r requirements.txt
jupyter notebook churn_survival_analysis.ipynb

