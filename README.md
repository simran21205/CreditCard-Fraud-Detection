# CreditCard-Fraud-Detection


A machine learning project to detect fraudulent credit card transactions. The dataset is highly imbalanced; Less than 0.2% of transactions are fraud, so the project focuses on handling that imbalance properly and evaluating models with the right metrics.
---------------------------------------------------------------------------------------------------------
**What This Project Does**
  1. Explores the dataset and visualizes class imbalance, transaction amounts, and fraud over time.
  2. Applies SMOTE to handle the imbalanced classes.
  3. Trains and compares three models: Logistic Regression, Random Forest, and XGBoost.
  4. Evaluates models using Precision, Recall, F1, ROC-AUC, and Precision-Recall curves.
  5. Tunes the decision threshold to maximize recall (catching more fraud).
  6. Estimates the business cost of false negatives vs false positives at each threshold.
  7. Saves the trained model and provides a ready-to-use prediction function.

  ---------------------------------------------------------------------------------------------------------
  **Dataset**
  
  - Source: [Kaggle — Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
  - 284,807 transactions | 492 fraud cases 
  - Dataset is not included in this repository — please download it from Kaggle
---------------------------------------------------------------------------------------------------------
## Results

The three models were trained on SMOTE-resampled data and evaluated on a held-out test set.
XGBoost performed best overall, achieving the highest recall while maintaining strong precision.

| Model | Precision | Recall | F1 | ROC-AUC |
|-------|-----------|--------|----|---------|
| Logistic Regression | ~0.87 | ~0.62 | ~0.73 | ~0.97 |
| Random Forest | ~0.96 | ~0.79 | ~0.87 | ~0.98 |
| XGBoost | ~0.94 | ~0.84 | ~0.89 | ~0.98 |

A few things worth noting:

- Accuracy was not used as a metric since the dataset is heavily imbalanced. A model that predicts
  every transaction as legitimate would still achieve 99.8% accuracy but catch zero fraud cases.
- The Precision-Recall curve was prioritized over the ROC curve for the same reason.
- The default decision threshold of 0.5 was adjusted to 0.3 to improve recall, since missing a
  fraudulent transaction is more costly than a false alarm.
- A cost analysis was performed assuming a missed fraud costs $122 and a false alert costs $5,
  and the threshold was tuned accordingly to minimize total business cost.
