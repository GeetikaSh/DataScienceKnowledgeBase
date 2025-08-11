# Precision, Recall, and F1 Score | Classification Metrics

## 1. **Precision**
- **Definition:** Precision measures how many of the predicted positive results are actually correct.
- **Formula:**

$\text{Precision} = \frac{TP}{TP + FP}$

- **Where:**
  - **TP (True Positive):** Correctly predicted positive cases.
  - **FP (False Positive):** Incorrectly predicted positive cases.
- **Use Case:** Useful when the **cost of false positives is high** (e.g., spam detection).

---

## 2. **Recall** (a.k.a. Sensitivity or True Positive Rate)
- **Definition:** Recall measures how many of the actual positive cases were correctly identified.
- **Formula:**

$\text{Recall} = \frac{TP}{TP + FN}$

- **Where:**
  - **FN (False Negative):** Missed positive cases.
- **Use Case:** Useful when **missing a positive case is costly** (e.g., disease detection).

---

## 3. **F1 Score**
- **Definition:** The harmonic mean of Precision and Recall. It balances both metrics.
- **Formula:**

$\text{F1 Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$

- **Use Case:** Useful when there is an **imbalance between classes** and both false positives and false negatives are important.

---

## 4. **Example Confusion Matrix**
|               | Predicted Positive | Predicted Negative |
|---------------|--------------------|--------------------|
| **Actual Positive** | TP = 70             | FN = 30             |
| **Actual Negative** | FP = 10             | TN = 90             |

- **Precision:**

$\frac{70}{70 + 10} = 0.875$

- **Recall:**

$\frac{70}{70 + 30} = 0.70$

- **F1 Score:**

$2 \times \frac{0.875 \times 0.70}{0.875 + 0.70} \approx 0.778$

---

✅ **Key Takeaway:**  
- Use **Precision** when **false positives** are more critical.  
- Use **Recall** when **false negatives** are more critical.  
- Use **F1 Score** when **both** matter and there’s **class imbalance**.
