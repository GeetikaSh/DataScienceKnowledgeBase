# Model Evaluation: Notes

Evaluating model performance is crucial to understand how well your model generalizes to unseen data and to compare different models. Here are key steps and metrics:

## 1. **Split Your Data**
- **Training Set:** Used to train the model.
- **Validation Set:** Used for tuning hyperparameters.
- **Test Set:** Used for final evaluation.

## 2. **Choose Appropriate Metrics**
- **Classification:** Accuracy, Precision, Recall, F1-score, ROC-AUC, Confusion Matrix.
- **Regression:** Mean Squared Error (MSE), Mean Absolute Error (MAE), R² Score.
- **Clustering:** Silhouette Score, Adjusted Rand Index, Homogeneity.

## 3. **Cross-Validation**
- Use k-fold cross-validation to assess model stability and reduce overfitting.

## 4. **Error Analysis**
- Analyze misclassified or poorly predicted samples to identify model weaknesses.

## 5. **Visualizations**
- ROC curves, Precision-Recall curves, Residual plots, Confusion matrices.

## 6. **Other Considerations**
- **Overfitting/Underfitting:** Compare train vs. test performance.
- **Domain-specific metrics:** Use metrics relevant to your application (e.g., BLEU for NLP).

## 7. **Reporting**
- Summarize results with tables and plots.
- Compare with baseline models.

**Tip:** Always use unseen test data for final evaluation to