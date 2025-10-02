# Measures of Central Tendency

Measures of central tendency represent the center point or typical value of a dataset. These are fundamental to understanding data distribution.

## Mean (Average)

The arithmetic mean is the sum of all values divided by the number of values.

**Formula:**
```
Mean (μ or x̄) = (Σ xi) / n
```

Where:
- Σ xi = Sum of all values
- n = Number of observations

### Properties
- Sensitive to outliers
- Uses all data points
- Can be misleading with skewed distributions

### Example
Dataset: [10, 15, 20, 25, 30]
Mean = (10 + 15 + 20 + 25 + 30) / 5 = 20

### Use Cases in Data Science
- Calculating average customer lifetime value
- Mean prediction error in regression models
- Average response time in system performance analysis

## Median

The middle value when data is ordered from smallest to largest.

### Properties
- Robust to outliers
- Better for skewed distributions
- May not represent actual data point

### Calculation
- **For odd n:** Middle value at position (n+1)/2
- **For even n:** Average of two middle values

### Example
- **Odd:** [10, 15, 20, 25, 30] → Median = 20
- **Even:** [10, 15, 20, 25] → Median = (15 + 20) / 2 = 17.5

### Use Cases
- Median household income (less affected by extremely high incomes)
- Median response time in web applications
- Real estate price analysis

## Mode

The most frequently occurring value in a dataset.

### Properties
- Can have multiple modes (bimodal, multimodal)
- May not exist for all datasets
- Useful for categorical data

### Example
[2, 3, 3, 5, 5, 5, 7, 8] → Mode = 5

### Use Cases
- Most common product size sold
- Most frequent customer complaint category
- Peak traffic hour identification

## Comparison and When to Use Each

| Measure | Best For | Limitation |
|---------|----------|------------|
| Mean | Normally distributed data | Sensitive to outliers |
| Median | Skewed distributions | Doesn't use all data |
| Mode | Categorical data | May not be unique |

## Python Implementation

```python
import pandas as pd
import numpy as np

# Calculate central tendency
data = [10, 15, 20, 25, 30]

mean = np.mean(data)
median = np.median(data)
mode = pd.Series(data).mode()[0]

print(f"Mean: {mean}")
print(f"Median: {median}")
print(f"Mode: {mode}")
```
