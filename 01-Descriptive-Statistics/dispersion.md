# Measures of Dispersion (Variability)

Dispersion measures describe the spread or variability in a dataset. They help us understand how data points differ from the central tendency.

## Range

The difference between maximum and minimum values.

**Formula:**
```
Range = Maximum value - Minimum value
```

### Properties
- Simple to calculate
- Highly sensitive to outliers
- Doesn't account for distribution

### Example
[10, 15, 20, 25, 100] → Range = 100 - 10 = 90

## Variance

The average of squared differences from the mean.

### Population Variance
```
σ² = Σ(xi - μ)² / N
```

### Sample Variance
```
s² = Σ(xi - x̄)² / (n - 1)
```

### Properties
- Always non-negative
- Units are squared
- Sensitive to outliers

### Example
Dataset: [2, 4, 6, 8, 10]
Mean = 6
Variance = [(2-6)² + (4-6)² + (6-6)² + (8-6)² + (10-6)²] / 5
         = [16 + 4 + 0 + 4 + 16] / 5 = 8

## Standard Deviation

The square root of variance, representing average distance from the mean.

**Formula:**
```
σ = √(σ²)  or  s = √(s²)
```

### Properties
- Same units as original data
- Interpretable measure of spread
- Most commonly used dispersion measure

### Example
From previous variance example:
Standard Deviation = √8 ≈ 2.83

### Use Cases
- Risk assessment in finance (volatility)
- Quality control in manufacturing
- Model performance evaluation (RMSE)

## Interquartile Range (IQR)

The difference between the 75th percentile (Q3) and 25th percentile (Q1).

**Formula:**
```
IQR = Q3 - Q1
```

### Properties
- Robust to outliers
- Measures middle 50% of data
- Used in boxplot construction

### Example
Dataset: [1, 3, 5, 7, 9, 11, 13, 15, 17]
Q1 (25th percentile) = 5
Q3 (75th percentile) = 13
IQR = 13 - 5 = 8

### Outlier Detection
Outliers are typically defined as:
- Below Q1 - 1.5 × IQR
- Above Q3 + 1.5 × IQR

## Coefficient of Variation (CV)

A relative measure of dispersion, useful for comparing variability across datasets with different units or scales.

**Formula:**
```
CV = (σ / μ) × 100%
```

### Properties
- Unit-less (percentage)
- Useful for comparing variability
- Only meaningful for ratio scale data

### Example
Dataset A: Mean = 50, SD = 5 → CV = (5/50) × 100% = 10%
Dataset B: Mean = 200, SD = 20 → CV = (20/200) × 100% = 10%
Both have equal relative variability

## Comparison Table

| Measure | Robust to Outliers | Units | Use Case |
|---------|-------------------|-------|----------|
| Range | No | Same as data | Quick spread check |
| Variance | No | Squared | Statistical calculations |
| Std Dev | No | Same as data | Most common measure |
| IQR | Yes | Same as data | Outlier detection |
| CV | No | Percentage | Cross-dataset comparison |

## Python Implementation

```python
import numpy as np
import pandas as pd

data = [2, 4, 6, 8, 10]

# Range
data_range = np.max(data) - np.min(data)

# Variance
variance = np.var(data, ddof=1)  # ddof=1 for sample variance

# Standard Deviation
std_dev = np.std(data, ddof=1)

# IQR
Q1 = np.percentile(data, 25)
Q3 = np.percentile(data, 75)
IQR = Q3 - Q1

# Coefficient of Variation
mean = np.mean(data)
cv = (std_dev / mean) * 100

print(f"Range: {data_range}")
print(f"Variance: {variance}")
print(f"Standard Deviation: {std_dev}")
print(f"IQR: {IQR}")
print(f"CV: {cv}%")
```

## When to Use Each Measure

1. **Use Range** when you need a quick, simple measure of spread
2. **Use Variance** in statistical calculations and hypothesis testing
3. **Use Standard Deviation** for most practical interpretations
4. **Use IQR** when dealing with skewed data or outliers
5. **Use CV** when comparing datasets with different scales or units
