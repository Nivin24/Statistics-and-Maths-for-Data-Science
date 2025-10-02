# Distribution Shape Measures

Distribution shape measures help us understand the symmetry and tail behavior of data distributions.

## Skewness

Skewness measures the asymmetry of the distribution.

### Types of Skewness

#### 1. Positive Skew (Right-skewed)
- **Definition:** Tail extends to the right
- **Relationship:** Mean > Median > Mode
- **Examples:**
  - Income distribution
  - Housing prices
  - Response times
  - Asset prices

#### 2. Negative Skew (Left-skewed)
- **Definition:** Tail extends to the left
- **Relationship:** Mode > Median > Mean
- **Examples:**
  - Age at retirement
  - Exam scores with ceiling effect
  - Lifespan data

#### 3. Zero Skew (Symmetric)
- **Definition:** Balanced distribution
- **Relationship:** Mean ≈ Median ≈ Mode
- **Examples:**
  - Heights (approximately)
  - IQ scores (approximately)
  - Many natural phenomena

### Interpreting Skewness Values

| Skewness Value | Interpretation |
|----------------|----------------|
| \|Skewness\| < 0.5 | Fairly symmetric |
| 0.5 < \|Skewness\| < 1 | Moderately skewed |
| \|Skewness\| > 1 | Highly skewed |

### Formula

```
Skewness = [n / ((n-1)(n-2))] × Σ[(xi - x̄) / s]³
```

Where:
- n = sample size
- xi = individual values
- x̄ = mean
- s = standard deviation

## Kurtosis

Kurtosis measures the "tailedness" or peakedness of the distribution.

### Types of Kurtosis

#### 1. Leptokurtic (Kurtosis > 3)
- Heavy tails, sharp peak
- More outliers than normal distribution
- High risk in financial terms
- Examples: Stock returns, earthquake magnitudes

#### 2. Mesokurtic (Kurtosis = 3)
- Normal distribution
- Moderate tails and peak
- Baseline for comparison

#### 3. Platykurtic (Kurtosis < 3)
- Light tails, flat peak
- Fewer outliers than normal distribution
- More uniform spread
- Examples: Uniform distribution

### Excess Kurtosis

Often, **excess kurtosis** is used (Kurtosis - 3):
- Excess Kurtosis > 0: Leptokurtic
- Excess Kurtosis = 0: Mesokurtic (Normal)
- Excess Kurtosis < 0: Platykurtic

### Formula

```
Kurtosis = [n(n+1) / ((n-1)(n-2)(n-3))] × Σ[(xi - x̄) / s]⁴
```

## Practical Implications

### For Skewness

1. **Data Transformation**
   - Positive skew: Use log transformation
   - Negative skew: Use square or exponential transformation

2. **Model Selection**
   - Highly skewed data may require non-parametric methods
   - Consider median instead of mean for central tendency

3. **Feature Engineering**
   - Create binned categories
   - Apply Box-Cox transformation

### For Kurtosis

1. **Risk Assessment**
   - High kurtosis = Higher risk of extreme values
   - Important in finance and insurance

2. **Outlier Detection**
   - Leptokurtic distributions have more outliers
   - Adjust outlier detection thresholds accordingly

3. **Model Assumptions**
   - Many statistical tests assume normality (mesokurtic)
   - Check kurtosis before applying parametric tests

## Visual Identification

### Using Histograms
- **Skewness:** Look at tail direction
- **Kurtosis:** Look at peak sharpness and tail thickness

### Using Q-Q Plots
- Points follow diagonal line = Normal distribution
- S-shaped curve = Skewed distribution
- Curved tails = Non-normal kurtosis

## Python Implementation

```python
import numpy as np
import pandas as pd
from scipy import stats
import matplotlib.pyplot as plt
import seaborn as sns

# Sample data
data = np.random.exponential(2, 1000)  # Right-skewed data

# Calculate skewness and kurtosis
skewness = stats.skew(data)
kurtosis = stats.kurtosis(data)  # This returns excess kurtosis

print(f"Skewness: {skewness:.3f}")
print(f"Excess Kurtosis: {kurtosis:.3f}")

# Using pandas
df = pd.DataFrame({'values': data})
print(f"Pandas Skewness: {df['values'].skew():.3f}")
print(f"Pandas Kurtosis: {df['values'].kurtosis():.3f}")

# Visualization
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

# Histogram
axes[0].hist(data, bins=30, edgecolor='black')
axes[0].set_title('Distribution Shape')
axes[0].set_xlabel('Value')
axes[0].set_ylabel('Frequency')

# Q-Q Plot
stats.probplot(data, dist="norm", plot=axes[1])
axes[1].set_title('Q-Q Plot')

plt.tight_layout()
plt.show()
```

## Handling Non-Normal Distributions

### Transformations

1. **Log Transformation** (for positive skew)
   ```python
   log_data = np.log(data + 1)  # +1 to handle zeros
   ```

2. **Square Root Transformation** (for moderate skew)
   ```python
   sqrt_data = np.sqrt(data)
   ```

3. **Box-Cox Transformation** (automatic)
   ```python
   from scipy import stats
   transformed_data, lambda_param = stats.boxcox(data + 1)
   ```

4. **Yeo-Johnson Transformation** (handles negative values)
   ```python
   from sklearn.preprocessing import PowerTransformer
   pt = PowerTransformer(method='yeo-johnson')
   transformed_data = pt.fit_transform(data.reshape(-1, 1))
   ```

## Common Distributions and Their Properties

| Distribution | Skewness | Kurtosis | Use Case |
|--------------|----------|----------|----------|
| Normal | 0 | 3 | General modeling |
| Exponential | 2 | 9 | Waiting times |
| Uniform | 0 | 1.8 | Random sampling |
| Log-normal | Positive | High | Income, stock prices |
| T-distribution | 0 | >3 | Small samples |

## Key Takeaways

1. **Skewness** tells you about distribution asymmetry
2. **Kurtosis** tells you about tail behavior and outliers
3. Both are important for:
   - Choosing appropriate statistical tests
   - Understanding data characteristics
   - Detecting potential issues in data
   - Feature engineering in ML models
4. Always visualize your data along with calculating these metrics
