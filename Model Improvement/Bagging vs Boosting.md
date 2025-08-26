## Bagging (Bootstrap Aggregating):
- Multiple models (like decision trees) are trained in parallel on different random samples of the dataset (with replacement).
- Predictions are averaged (regression) or voted (classification).
- Goal: reduce variance and avoid overfitting.
- Example: Random Forest.

## Boosting:
- Models are trained sequentially. Each new model focuses more on the errors (misclassified points) of the previous models.
- Predictions are combined with weighted averages.
- Goal: reduce bias and build a strong learner from weak learners.
- Example: XGBoost, AdaBoost, LightGBM.