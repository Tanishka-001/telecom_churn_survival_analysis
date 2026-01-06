# Telecom Churn Survival Analysis 

Predicts **churn timing** (C-index **0.846**). Fiber + e-check = danger zone.

## Results
| Metric       | Score  |
|--------------|--------|
| **Test C-Index** | **0.846** |
| **CV C-Index**   | **0.858**  |

**Survival Curve**

![image alt](https://github.com/Tanishka-001/telecom_churn_survival_analysis/blob/44f823044c46bc2f791c232d93da1bb3a1009d65/survival_curve.png)


**![Cox Hazards]()**

## Insights
- **Risk:** Fiber Optic (HR **1.38**), Electronic Check (**1.56**)
- **Safe:** TechSupport (**0.65**), 2yr Contract (**0.31**)

## Setup
```bash
pip install -r requirements.txt
jupyter notebook churn_survival_analysis.ipynb

