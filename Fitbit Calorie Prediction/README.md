# Fitbit Calorie Prediction

Predict daily calories burned using Fitbit activity data with machine learning.

---

## Executive Summary

- Built a calorie-prediction model using Fitbit activity data.  
- Tuned Random Forest improved MAE by **36.7% over baseline**.  
- Provided actionable insights on behavioral drivers of calorie burn.  
- Model is saved and ready for deployment (`fitbit_calorie_model.pkl`).  

---

## Technologies & Libraries

- **Python** – Core programming  
- **Pandas & NumPy** – Data manipulation  
- **Matplotlib & Seaborn** – Visualization  
- **Scikit-learn** – Machine learning (Linear Regression, Ridge, Random Forest, Gradient Boosting)  
- **Joblib** – Model serialization  

---

## Dataset

- **Source:** Fitbit daily activity data  
- **Features:**  
  - Steps (`TotalSteps`)  
  - Distance (`TotalDistance`)  
  - Active minutes (`VeryActiveMinutes`, `FairlyActiveMinutes`, `LightlyActiveMinutes`)  
  - Sedentary minutes (`SedentaryMinutes`)  
  - Calories burned (`Calories`)  

- **Feature Engineering:**  
  - Created `TotalActiveMinutes` = sum of all active minutes.  

---

## Modeling Approach

1. **Train/Test Split** – 80/20 split to evaluate performance on unseen data.  
2. **Baseline Model** – Mean calorie value as reference.  
3. **Model Training** – Linear Regression, Ridge Regression, Random Forest, Gradient Boosting.  
4. **Model Comparison** – Evaluated using MAE, RMSE, and R².  
5. **Hyperparameter Tuning** – GridSearchCV on Random Forest for optimal parameters.  
6. **Cross-Validation** – Confirmed model stability with 5-fold CV.  
7. **Feature Importance** – Identified behavioral drivers of calorie burn.  
8. **Residual Analysis** – Checked bias and prediction errors.  
9. **Deployment** – Model saved for future use.  

---

## Key Results

| Model              | MAE     | RMSE    | R²       |
|------------------|--------|--------|----------|
| Baseline          | 552.27 | –      | –        |
| Linear Regression | 414.09 | 514.09 | 0.44     |
| Ridge Regression  | 414.23 | 514.15 | 0.44     |
| Random Forest     | 350.00 | 472.51 | 0.53     |
| Gradient Boosting | 360.31 | 484.53 | 0.50     |

- **Best Model:** Random Forest  
- **MAE Improvement Over Baseline:** 36.7%  
- **Cross-Validated MAE:** 341.88  

---

## Insights

- Total distance traveled was the strongest predictor of calories burned.  
- Steps and total active minutes positively associated with calorie burn.  
- Sedentary time negatively impacted calories burned.  

---

## Limitations

- Fitbit data is device-estimated; may contain measurement errors.  
- No demographic or physiological features included (age, weight, gender).  
- Daily aggregation loses temporal patterns.  

---

## Next Steps

- Try **XGBoost** or **LightGBM** for potentially better performance.  
- Include **time-series or session-level activity features**.  
- Build a **REST API** for deployment to web or mobile apps.  
- Apply **SHAP values** for deeper interpretability of feature contributions.  

---

## Usage

```python
import joblib
model = joblib.load("fitbit_calorie_model.pkl")
preds = model.predict(X_new)  # X_new: new activity data