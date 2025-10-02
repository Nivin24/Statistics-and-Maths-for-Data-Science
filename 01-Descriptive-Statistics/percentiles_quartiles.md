# Percentiles and Quartiles

Percentiles and quartiles are positional measures that divide data into equal parts, providing insights into the distribution and spread of values.

## 📚 Table of Contents
1. [Understanding Percentiles](#understanding-percentiles)
2. [Quartiles](#quartiles)
3. [Five-Number Summary](#five-number-summary)
4. [Interquartile Range (IQR)](#interquartile-range-iqr)
5. [Calculation Methods](#calculation-methods)
6. [Python Implementation](#python-implementation)
7. [Practical Applications](#practical-applications)
8. [Common Pitfalls](#common-pitfalls)
9. [Summary](#summary)

## Understanding Percentiles

### Definition
A **percentile** is a value below which a certain percentage of data points fall. The k-th percentile is the value below which k% of the data lies.

### Key Characteristics
- Range from 0th to 100th percentile
- Divide data into 100 equal parts
- Robust to outliers (less sensitive than mean)
- Useful for understanding relative position

### Common Percentiles
- **P25 (25th percentile)**: First quartile (Q1)
- **P50 (50th percentile)**: Median (Q2)
- **P75 (75th percentile)**: Third quartile (Q3)
- **P90 (90th percentile)**: Often used for outlier detection
- **P99 (99th percentile)**: Extreme values threshold

## Quartiles

### Definition
Quartiles divide the dataset into four equal parts, each containing 25% of the data.

### The Four Quartiles
1. **Q1 (First Quartile)**: 25th percentile
   - 25% of data below this value
   - Lower boundary of middle 50%

2. **Q2 (Second Quartile)**: 50th percentile (Median)
   - 50% of data below this value
   - Middle value of the dataset

3. **Q3 (Third Quartile)**: 75th percentile
   - 75% of data below this value
   - Upper boundary of middle 50%

4. **Q4**: Maximum value (100th percentile)

### Quartile Interpretation
```
Minimum  Q1    Q2(Median)  Q3    Maximum
   |-----|-------|-------|-----|   
   25%    25%     25%    25%
```

## Five-Number Summary

The five-number summary provides a complete description of data distribution:

1. **Minimum**: Smallest value
2. **Q1**: First quartile (25th percentile)
3. **Median (Q2)**: Middle value (50th percentile)
4. **Q3**: Third quartile (75th percentile)
5. **Maximum**: Largest value

### Uses
- Foundation for box plots
- Quick distribution overview
- Outlier detection
- Comparing multiple datasets

## Interquartile Range (IQR)

### Formula
```
IQR = Q3 - Q1
```

### Characteristics
- Measures spread of middle 50% of data
- Robust to outliers
- Used in outlier detection
- Always non-negative

### Outlier Detection Rule
- **Lower Outlier Boundary**: Q1 - 1.5 × IQR
- **Upper Outlier Boundary**: Q3 + 1.5 × IQR
- Values outside these boundaries are potential outliers

## Calculation Methods

### Method 1: Linear Interpolation (Most Common)
1. Sort data in ascending order
2. Calculate position: `position = (percentile/100) × (n-1) + 1`
3. If position is integer, use that value
4. If not, interpolate between adjacent values

### Method 2: Nearest Rank
1. Sort data in ascending order
2. Calculate rank: `rank = ceiling((percentile/100) × n)`
3. Use value at that rank

### Example Calculation
Data: [1, 3, 5, 7, 9, 11, 13, 15]

**For Q1 (25th percentile):**
- Position = (25/100) × (8-1) + 1 = 2.75
- Interpolate between 2nd (3) and 3rd (5) values
- Q1 = 3 + 0.75 × (5-3) = 4.5

**For Q3 (75th percentile):**
- Position = (75/100) × (8-1) + 1 = 6.25
- Interpolate between 6th (11) and 7th (13) values
- Q3 = 11 + 0.25 × (13-11) = 11.5

## Python Implementation

### Using NumPy
```python
import numpy as np

# Sample data
data = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]

# Calculate percentiles
q1 = np.percentile(data, 25)
q2 = np.percentile(data, 50)  # median
q3 = np.percentile(data, 75)

# Calculate IQR
iqr = q3 - q1

print(f"Q1 (25th percentile): {q1}")
print(f"Q2 (50th percentile - Median): {q2}")
print(f"Q3 (75th percentile): {q3}")
print(f"IQR: {iqr}")

# Custom percentiles
p90 = np.percentile(data, 90)
p95 = np.percentile(data, 95)
print(f"90th percentile: {p90}")
print(f"95th percentile: {p95}")
```

### Using Pandas
```python
import pandas as pd

# Create DataFrame
df = pd.DataFrame({'values': [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]})

# Calculate quartiles
quartiles = df['values'].quantile([0.25, 0.5, 0.75])
print("Quartiles:")
print(quartiles)

# Five-number summary
summary = df['values'].describe()
print("\nFive-number summary:")
print(summary[['min', '25%', '50%', '75%', 'max']])

# IQR calculation
q1 = df['values'].quantile(0.25)
q3 = df['values'].quantile(0.75)
iqr = q3 - q1
print(f"\nIQR: {iqr}")
```

### Outlier Detection Function
```python
def detect_outliers_iqr(data):
    """
    Detect outliers using IQR method
    """
    q1 = np.percentile(data, 25)
    q3 = np.percentile(data, 75)
    iqr = q3 - q1
    
    lower_bound = q1 - 1.5 * iqr
    upper_bound = q3 + 1.5 * iqr
    
    outliers = [x for x in data if x < lower_bound or x > upper_bound]
    
    return {
        'outliers': outliers,
        'lower_bound': lower_bound,
        'upper_bound': upper_bound,
        'q1': q1,
        'q3': q3,
        'iqr': iqr
    }

# Example usage
data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 100]  # 100 is an outlier
result = detect_outliers_iqr(data)
print(f"Outliers detected: {result['outliers']}")
print(f"Valid range: [{result['lower_bound']:.2f}, {result['upper_bound']:.2f}]")
```

### Visualization with Box Plot
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Create box plot to visualize quartiles
plt.figure(figsize=(10, 6))

# Sample datasets
np.random.seed(42)
data1 = np.random.normal(50, 15, 100)
data2 = np.random.exponential(20, 100)
data3 = np.random.uniform(10, 90, 100)

# Create DataFrame
df = pd.DataFrame({
    'Normal': data1,
    'Exponential': data2,
    'Uniform': data3
})

# Box plot
sns.boxplot(data=df)
plt.title('Box Plot Showing Quartiles and Outliers')
plt.ylabel('Values')
plt.xlabel('Distribution Type')

# Add quartile annotations
for i, col in enumerate(df.columns):
    q1 = df[col].quantile(0.25)
    q2 = df[col].quantile(0.50)
    q3 = df[col].quantile(0.75)
    
    plt.text(i-0.3, q1, f'Q1={q1:.1f}', fontsize=8)
    plt.text(i-0.3, q2, f'Q2={q2:.1f}', fontsize=8, weight='bold')
    plt.text(i-0.3, q3, f'Q3={q3:.1f}', fontsize=8)

plt.tight_layout()
plt.show()
```

## Practical Applications

### 1. Performance Analysis
```python
# Analyze student test scores
scores = [65, 72, 78, 81, 85, 87, 89, 92, 94, 96, 98]

q1 = np.percentile(scores, 25)
q2 = np.percentile(scores, 50)
q3 = np.percentile(scores, 75)

print(f"Bottom 25% scored below: {q1}")
print(f"Top 25% scored above: {q3}")
print(f"Middle 50% scored between: {q1} and {q3}")
```

### 2. Salary Analysis
```python
# Company salary quartiles
salaries = [35000, 42000, 48000, 55000, 62000, 68000, 75000, 82000, 95000, 120000]

quartiles = np.percentile(salaries, [25, 50, 75])
print(f"Salary Quartiles:")
print(f"Q1 (25th percentile): ${quartiles[0]:,.0f}")
print(f"Q2 (Median): ${quartiles[1]:,.0f}")
print(f"Q3 (75th percentile): ${quartiles[2]:,.0f}")
```

### 3. Quality Control
```python
# Manufacturing tolerance analysis
measurements = [99.2, 99.5, 99.8, 100.1, 100.2, 100.3, 100.4, 100.6, 100.8, 101.2]

# Control limits based on quartiles
q1 = np.percentile(measurements, 25)
q3 = np.percentile(measurements, 75)
iqr = q3 - q1

lower_control = q1 - 1.5 * iqr
upper_control = q3 + 1.5 * iqr

print(f"Quality Control Limits: [{lower_control:.2f}, {upper_control:.2f}]")
```

## Common Pitfalls

### 1. Small Sample Sizes
- Percentiles less reliable with small datasets
- Consider confidence intervals
- Use caution with extreme percentiles (P1, P99)

### 2. Different Calculation Methods
- Various software may use different interpolation methods
- Results can vary slightly
- Document which method you're using

### 3. Misinterpretation
```python
# WRONG: "75% of values are Q3"
# CORRECT: "75% of values are below Q3"

# WRONG: Using percentiles for normally distributed data exclusively
# CORRECT: Percentiles work for any distribution
```

### 4. Outlier Detection Limitations
- IQR method assumes normal-like distribution
- May not work well for highly skewed data
- Consider other methods for non-normal distributions

## Summary

### Key Points
1. **Percentiles** divide data into 100 equal parts
2. **Quartiles** are special percentiles (25th, 50th, 75th)
3. **Five-number summary** provides complete distribution overview
4. **IQR** measures middle 50% spread and detects outliers
5. **Robust** to outliers and distribution shape

### When to Use
- **Data exploration** and initial analysis
- **Outlier detection** and data cleaning
- **Performance benchmarking** and comparisons
- **Non-normal distributions** where mean/std aren't appropriate
- **Reporting** to non-technical stakeholders

### Formula Quick Reference
```
Percentile Position = (P/100) × (n-1) + 1
IQR = Q3 - Q1
Outlier Bounds = Q1 - 1.5×IQR, Q3 + 1.5×IQR
```

---

**Next Steps**: 
- Practice with [visualization.md](visualization.md) for visual representation
- Explore [practical_applications.md](practical_applications.md) for real-world examples
- Review [pitfalls_best_practices.md](pitfalls_best_practices.md) for implementation guidelines
