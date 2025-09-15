# Binning in Feature Engineering

Binning (or discretization) is the process of converting continuous variables into discrete bins or intervals. This technique can help improve model performance, handle outliers, and make data more interpretable.

## Why Use Binning?
- Reduces the impact of outliers
- Simplifies models by grouping values
- Can reveal hidden patterns
- Useful for decision tree algorithms

## Types of Binning
- **Equal-width binning:** Divides the range into intervals of equal size
- **Equal-frequency binning:** Each bin has approximately the same number of observations
- **Custom binning:** User-defined intervals based on domain knowledge

## Python Pseudocode Example
```python
# Equal-width binning using pandas
import pandas as pd

data = pd.DataFrame({'age': [15, 22, 37, 45, 52, 63, 70]})

# Create 3 bins
bins = [0, 30, 50, 100]
labels = ['Young', 'Middle-aged', 'Senior']
data['age_group'] = pd.cut(data['age'], bins=bins, labels=labels)

print(data)
# Output:
#    age    age_group
# 0   15        Young
# 1   22        Young
# 2   37  Middle-aged
# 3   45  Middle-aged
# 4   52       Senior
# 5   63       Senior
# 6   70       Senior
```

## SQL Pseudocode Example
```sql
-- Equal-width binning for age
SELECT age,
  CASE
    WHEN age < 30 THEN 'Young'
    WHEN age >= 30 AND age < 50 THEN 'Middle-aged'
    ELSE 'Senior'
  END AS age_group
FROM people;
```

## Best Practices
- Choose bin edges carefully to avoid information loss
- Use domain knowledge for custom bins
- Visualize distributions before and after binning

---

> "Binning transforms continuous data into categorical, making patterns easier to spot and models easier to interpret."