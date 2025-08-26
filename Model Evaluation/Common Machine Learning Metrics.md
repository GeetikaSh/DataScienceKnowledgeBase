# Overview of Common Machine Learning Metrics

This document provides a concise overview of the most common evaluation metrics used to assess the performance of machine learning models. Understanding these metrics is crucial for selecting the best model for a given task and for communicating its performance effectively.

## Table of Contents

- [Classification Metrics](#classification-metrics)
    - [Accuracy](#accuracy)
    - [Precision](#precision)
    - [Recall (Sensitivity)](#recall-sensitivity)
    - [F1-Score](#f1-score)
- [Regression Metrics](#regression-metrics)
    - [R-squared ($R^2$)](#r-squared-r2)
    - [Root Mean Square Error (RMSE)](#root-mean-square-error-rmse)

---

## Classification Metrics

These metrics are used to evaluate models that predict a categorical output (e.g., "spam" or "not spam," "disease" or "no disease").

### Accuracy

**Definition:** The proportion of total predictions that were correct. It is a simple and intuitive metric but can be misleading for imbalanced datasets.

$$
\text{Accuracy} = \frac{\text{Number of Correct Predictions}}{\text{Total Number of Predictions}}
$$

**Use Case:** Best used when the classes in the dataset are roughly equal in size.

---

### Precision

**Definition:** Of all the instances the model predicted as positive, how many were actually positive? It measures the model's ability to avoid false positives.

$$
\text{Precision} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Positives}}
$$

**Use Case:** Crucial when the cost of a false positive is high. For example, in a medical diagnosis, a false positive might lead to unnecessary treatment.

---

### Recall (Sensitivity)

**Definition:** Of all the actual positive instances, how many did the model correctly identify? It measures the model's ability to find all positive instances and avoid false negatives.

$$
\text{Recall} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}
$$

**Use Case:** Crucial when the cost of a false negative is high. For example, in fraud detection, a false negative means a fraudulent transaction is missed.

---

### F1-Score

**Definition:** The harmonic mean of Precision and Recall. It provides a single score that balances both metrics, making it a good choice for imbalanced classification problems.

$$
\text{F1-Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$

**Use Case:** Ideal when there is an uneven class distribution, as it gives a better measure of the model's performance than accuracy.

---

## Regression Metrics

These metrics are used to evaluate models that predict a continuous numerical output (e.g., house prices, temperature).

### R-squared ($R^2$)

**Definition:** Also known as the coefficient of determination, it measures the proportion of the variance in the dependent variable that is predictable from the independent variable(s). A value of 1 indicates the model explains all the variability, while a value of 0 indicates the model explains none.

**Use Case:** Provides a quick sense of how well the model fits the data, but it can be misleading if the model is complex or has many features.

---

### Root Mean Square Error (RMSE)

**Definition:** The standard deviation of the residuals (prediction errors). It measures the average magnitude of the errors. Because the errors are squared before they are averaged, RMSE gives a higher weight to larger errors.

$$
\text{RMSE} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2}
$$

**Use Case:** Highly interpretable because the error is in the same units as the target variable. It's an excellent metric for understanding the typical prediction error.
