# Statistics and Maths for Data Science

A comprehensive repository covering fundamental mathematical and statistical concepts essential for Data Science, Machine Learning, and AI.

## 📁 Repository Structure

```
Statistics-and-Maths-for-Data-Science/
│
├── 01-Descriptive-Statistics/
│   ├── descriptive_statistics.md
│   ├── descriptive_statistics.ipynb
│   └── README.md
│
├── 02-Inferential-Statistics/
│   ├── inferential_statistics.md
│   ├── inferential_statistics.ipynb
│   └── README.md
│
├── 03-Probability/
│   ├── probability.md
│   ├── probability.ipynb
│   └── README.md
│
├── 04-Linear-Algebra/
│   ├── linear_algebra.md
│   ├── linear_algebra.ipynb
│   └── README.md
│
├── 05-Calculus/
│   ├── calculus.md
│   ├── calculus.ipynb
│   └── README.md
│
└── README.md
```

## 📚 Topics Covered

### 1. Descriptive Statistics
- Measures of Central Tendency
- Measures of Dispersion
- Data Visualization Techniques
- Distributions and Patterns

### 2. Inferential Statistics
- Hypothesis Testing
- Confidence Intervals
- Statistical Significance
- P-values and Test Statistics
- ANOVA and Chi-Square Tests

### 3. Probability
- Basic Probability Theory
- Conditional Probability
- Bayes' Theorem
- Probability Distributions
- Random Variables

### 4. Linear Algebra
- Vectors and Matrices
- Matrix Operations
- Eigenvalues and Eigenvectors
- Linear Transformations
- Applications in ML

### 5. Calculus
- Derivatives and Differentiation
- Partial Derivatives
- Gradients
- Optimization Techniques
- Applications in Deep Learning

---

## 📊 1. Descriptive Statistics

Descriptive statistics is the foundation of data analysis, providing methods to summarize, organize, and present data in a meaningful way. It helps us understand the basic features of a dataset and forms the basis for virtually every quantitative analysis.

### 1.1 Measures of Central Tendency

Measures of central tendency represent the center point or typical value of a dataset. These are fundamental to understanding data distribution.

#### Mean (Average)
The arithmetic mean is the sum of all values divided by the number of values.

**Formula:**
```
Mean (μ or x̄) = (Σ xi) / n
```
Where:
- Σ xi = Sum of all values
- n = Number of observations

**Properties:**
- Sensitive to outliers
- Uses all data points
- Can be misleading with skewed distributions

**Example:**
Dataset: [10, 15, 20, 25, 30]
Mean = (10 + 15 + 20 + 25 + 30) / 5 = 20

**Use Cases in Data Science:**
- Calculating average customer lifetime value
- Mean prediction error in regression models
- Average response time in system performance analysis

#### Median
The middle value when data is ordered from smallest to largest.

**Properties:**
- Robust to outliers
- Better for skewed distributions
- May not represent actual data point

**Calculation:**
- For odd n: Middle value at position (n+1)/2
- For even n: Average of two middle values

**Example:**
- Odd: [10, 15, 20, 25, 30] → Median = 20
- Even: [10, 15, 20, 25] → Median = (15 + 20) / 2 = 17.5

**Use Cases:**
- Median household income (less affected by extremely high incomes)
- Median response time in web applications
- Real estate price analysis

#### Mode
The most frequently occurring value in a dataset.

**Properties:**
- Can have multiple modes (bimodal, multimodal)
- May not exist for all datasets
- Useful for categorical data

**Example:**
[2, 3, 3, 5, 5, 5, 7, 8] → Mode = 5

**Use Cases:**
- Most common product size sold
- Most frequent customer complaint category
- Peak traffic hour identification

### 1.2 Measures of Dispersion (Variability)

Dispersion measures describe the spread or variability in a dataset.

#### Range
The difference between maximum and minimum values.

**Formula:**
```
Range = Maximum value - Minimum value
```

**Properties:**
- Simple to calculate
- Highly sensitive to outliers
- Doesn't account for distribution

**Example:**
[10, 15, 20, 25, 100] → Range = 100 - 10 = 90

#### Variance
The average of squared differences from the mean.

**Population Variance:**
```
σ² = Σ(xi - μ)² / N
```

**Sample Variance:**
```
s² = Σ(xi - x̄)² / (n - 1)
```

**Properties:**
- Always non-negative
- Units are squared
- Sensitive to outliers

**Example:**
Dataset: [2, 4, 6, 8, 10]
Mean = 6
Variance = [(2-6)² + (4-6)² + (6-6)² + (8-6)² + (10-6)²] / 5
         = [16 + 4 + 0 + 4 + 16] / 5 = 8

#### Standard Deviation
The square root of variance, representing average distance from the mean.

**Formula:**
```
σ = √(σ²)  or  s = √(s²)
```

**Properties:**
- Same units as original data
- Interpretable measure of spread
- Most commonly used dispersion measure

**Example:**
From previous variance example:
Standard Deviation = √8 ≈ 2.83

**Use Cases:**
- Risk assessment in finance (volatility)
- Quality control in manufacturing
- Model performance evaluation (RMSE)

#### Interquartile Range (IQR)
The difference between the 75th percentile (Q3) and 25th percentile (Q1).

**Formula:**
```
IQR = Q3 - Q1
```

**Properties:**
- Robust to outliers
- Measures middle 50% of data
- Used in boxplot construction

**Example:**
Dataset: [1, 3, 5, 7, 9, 11, 13, 15, 17]
Q1 (25th percentile) = 5
Q3 (75th percentile) = 13
IQR = 13 - 5 = 8

**Outlier Detection:**
Outliers are typically defined as:
- Below Q1 - 1.5 × IQR
- Above Q3 + 1.5 × IQR

### 1.3 Distribution Shape Measures

#### Skewness
Measures the asymmetry of the distribution.

**Types:**
- **Positive Skew (Right-skewed):** Tail extends to the right
  - Mean > Median > Mode
  - Example: Income distribution, housing prices

- **Negative Skew (Left-skewed):** Tail extends to the left
  - Mode > Median > Mean
  - Example: Age at retirement, exam scores with ceiling effect

- **Zero Skew (Symmetric):** Balanced distribution
  - Mean ≈ Median ≈ Mode
  - Example: Heights, IQ scores (approximately)

**Interpretation:**
- |Skewness| < 0.5: Fairly symmetric
- 0.5 < |Skewness| < 1: Moderately skewed
- |Skewness| > 1: Highly skewed

#### Kurtosis
Measures the "tailedness" or peakedness of the distribution.

**Types:**
- **Leptokurtic (Kurtosis > 3):** Heavy tails, sharp peak
- **Mesokurtic (Kurtosis = 3):** Normal distribution
- **Platykurtic (Kurtosis < 3):** Light tails, flat peak

### 1.4 Percentiles and Quartiles

**Percentiles:** Values below which a certain percentage of data falls.

**Common Percentiles:**
- P25 (Q1): 25th percentile - First quartile
- P50 (Q2): 50th percentile - Median
- P75 (Q3): 75th percentile - Third quartile
- P90, P95, P99: Used for performance metrics

**Use Cases:**
- Performance benchmarking
- Growth charts in pediatrics
- Latency metrics in system monitoring
- Academic ranking systems

### 1.5 Data Visualization Techniques

#### Histogram
- Shows frequency distribution of continuous data
- Bins group data into intervals
- Reveals distribution shape, central tendency, and spread

#### Box Plot (Box-and-Whisker Plot)
- Visual representation of five-number summary:
  - Minimum, Q1, Median, Q3, Maximum
- Identifies outliers
- Compares distributions across groups

#### Bar Chart
- Displays categorical data
- Shows frequency or proportion of categories
- Useful for comparisons

#### Scatter Plot
- Shows relationship between two continuous variables
- Identifies patterns, trends, and correlations
- Detects outliers and clusters

#### Line Plot
- Displays trends over time
- Shows continuous data progression
- Useful for time series analysis

### 1.6 Covariance and Correlation

#### Covariance
Measures how two variables change together.

**Formula:**
```
Cov(X,Y) = Σ[(xi - x̄)(yi - ȳ)] / (n - 1)
```

**Properties:**
- Positive: Variables increase together
- Negative: Variables move in opposite directions
- Zero: No linear relationship
- Scale-dependent (hard to interpret)

#### Correlation Coefficient (Pearson's r)
Standardized measure of linear relationship between two variables.

**Formula:**
```
r = Cov(X,Y) / (σx × σy)
```

**Properties:**
- Range: -1 to +1
- +1: Perfect positive correlation
- -1: Perfect negative correlation
- 0: No linear correlation

**Interpretation:**
- |r| < 0.3: Weak correlation
- 0.3 ≤ |r| < 0.7: Moderate correlation
- |r| ≥ 0.7: Strong correlation

**Important Note:** Correlation does not imply causation!

### 1.7 Practical Applications in Data Science

#### Exploratory Data Analysis (EDA)
1. Calculate summary statistics
2. Identify missing values and outliers
3. Visualize distributions
4. Examine relationships between variables
5. Check assumptions for modeling

#### Feature Engineering
- Standardization and normalization
- Handling skewed distributions (log transform)
- Creating categorical bins from continuous variables
- Identifying important features through correlation

#### Model Evaluation
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- R-squared statistic
- Confusion matrix statistics

### 1.8 Common Pitfalls and Best Practices

**Pitfalls to Avoid:**
1. Using mean for skewed distributions
2. Ignoring outliers without investigation
3. Assuming correlation implies causation
4. Comparing statistics without considering sample size
5. Misinterpreting standard deviation as standard error

**Best Practices:**
1. Always visualize data before analysis
2. Report multiple measures (mean + median + std)
3. Consider the context and domain knowledge
4. Document data cleaning and transformation steps
5. Use appropriate measures for data type (categorical vs continuous)
6. Check for and handle missing values appropriately
7. Validate findings with domain experts

### 1.9 Python Implementation Tips

**Essential Libraries:**
- NumPy: Numerical computations
- Pandas: Data manipulation and analysis
- Matplotlib/Seaborn: Visualization
- SciPy: Statistical functions

**Quick Reference:**
```python
import pandas as pd
import numpy as np

# Central tendency
df['column'].mean()
df['column'].median()
df['column'].mode()

# Dispersion
df['column'].var()
df['column'].std()
df['column'].quantile([0.25, 0.75])

# Summary statistics
df.describe()

# Correlation
df.corr()
```

---

## 🚀 Getting Started

Each topic folder contains:
- **Markdown files (.md)**: Theoretical explanations and formulas
- **Jupyter notebooks (.ipynb)**: Practical implementations with examples
- **README.md**: Quick reference and overview

## 📖 How to Use This Repository

1. **For Learning:** Start with the markdown files for theory, then practice with notebooks
2. **For Reference:** Use the quick reference guides in each README
3. **For Practice:** Work through the Jupyter notebooks with your own datasets

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Add more examples
- Improve explanations
- Fix errors or typos
- Suggest new topics

## 📝 License

This project is open source and available for educational purposes.

## 📧 Contact

For questions, suggestions, or discussions, please open an issue in this repository.

---

**Last Updated:** October 2025

**Status:** 🚧 Under active development - Descriptive Statistics section completed
