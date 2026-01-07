# UFC Fight Winner Prediction (Pre-Fight Data Only)

## Problem Statement
Can the winner of a UFC fight be predicted using only information available **before the fight**?

The goal of this project is to build an honest, leakage-free predictive model using fighter attributes and career statistics, without relying on any in-fight or post-fight data.

---

## Data Sources
This project uses publicly available UFC datasets from Kaggle (1994–2025), split across three main tables:

- **event_details.csv** – event-level information (date, location, winner)
- **fight_details.csv** – red/blue corner fighter identifiers and fight metadata
- **fighter_details.csv** – fighter attributes and career statistics

Only pre-fight information was used for modeling.

---

## Target Variable
The target variable is binary:

- `1` → Red corner fighter wins  
- `0` → Blue corner fighter wins  

The winner was derived by matching the event-level winner name to the red/blue fighter names for each bout.

---

## Feature Engineering
To avoid data leakage, all in-fight statistics (e.g., strikes landed, finish method, round, control time) were explicitly excluded.

Features were engineered as **differences between red and blue fighters**, including:

- Age difference
- Height and reach difference
- Experience difference (total fights)
- Win rate difference
- Career striking, grappling, and submission rate differences

Using difference features allows the model to learn **relative advantages**, which is more meaningful than raw values.

---

## Modeling Approach
A baseline **Logistic Regression** model was trained using:

- Numerical features: engineered pre-fight differences
- Categorical features: division, title fight indicator, fighter stances
- Median imputation for missing numerical values
- One-hot encoding for categorical variables

The dataset was split using an 80/20 train-test split with stratification.

---

## Results
- **Accuracy:** ~70.4%
- **ROC–AUC:** ~0.76

For context, a naive baseline that always predicts the red corner fighter achieves ~63% accuracy.  
The model significantly outperforms this baseline, indicating that pre-fight fighter attributes contain meaningful predictive signal.

---

## Limitations
- Fighter career statistics are aggregated and do not account for time decay.
- No betting odds or matchup-specific stylistic features were included.
- Sports outcomes are inherently noisy; perfect prediction is not possible.

---

## Future Improvements
- Apply time-weighted career statistics
- Evaluate tree-based models (e.g., Random Forest, Gradient Boosting)
- Perform temporal validation to better simulate real-world forecasting
- Add model explainability (e.g., SHAP values)

---

## Conclusion
This project demonstrates an end-to-end, leakage-aware data science workflow, from raw data integration to feature engineering, modeling, and evaluation. The focus is on correctness, interpretability, and real-world applicability rather than inflated metrics.
