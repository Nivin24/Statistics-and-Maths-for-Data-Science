# Data Visualization Techniques for Descriptive Statistics

Clear visualizations make distributions, patterns, and anomalies immediately understandable. This guide focuses on core plots for descriptive statistics, when to use them, and how to implement them in Python.

## Table of Contents
1. Principles of Effective Visualization
2. Histograms
3. Box Plots
4. Bar Charts
5. Scatter Plots
6. Line Plots
7. Density Plots (KDE)
8. Pair Plots and Correlation Heatmaps
9. Practical Tips and Pitfalls
10. Python Cookbook

## 1) Principles of Effective Visualization
- Match plot to data type (categorical vs numerical)
- Show distribution and uncertainty where relevant
- Use consistent scales and labels
- Avoid chartjunk; emphasize data, not decoration
- Provide context: titles, axes labels, units, legends

## 2) Histograms
- Purpose: Show distribution of a single numerical variable
- Good for: Central tendency, spread, skewness, modality
- Key parameters: bins, range, normalization
- Watch out: Over/under-binning can mislead

Example insights:
- Long right tail indicates positive skew
- Multiple peaks suggest mixture of sub-populations

## 3) Box Plots
- Purpose: Summarize distribution with five-number summary and outliers
- Good for: Comparing distributions across groups
- Robust to outliers; highlights them clearly

Interpretation:
- Box = IQR (Q1 to Q3), line = median
- Whiskers commonly extend to 1.5×IQR
- Points beyond whiskers are potential outliers

## 4) Bar Charts
- Purpose: Compare totals/counts across categories (categorical x-axis)
- Use counts or proportions; sort categories for readability
- Avoid using bar charts for continuous distributions (use histogram instead)

## 5) Scatter Plots
- Purpose: Relationship between two numerical variables
- Add trend line for quick pattern recognition
- Color/shape by category to reveal group differences

## 6) Line Plots
- Purpose: Trends over ordered index (time series)
- Avoid connecting unordered observations
- Consider smoothing (rolling mean) for noisy data

## 7) Density Plots (KDE)
- Purpose: Smooth estimate of distribution
- Complements histogram; bandwidth controls smoothness
- Overlay multiple KDEs to compare groups

## 8) Pair Plots and Correlation Heatmaps
- Pair plot: Grid of scatter/histogram/KDE for multivariate overview
- Heatmap: Color-coded correlation matrix for quick dependency scan
- Beware of spurious correlations; inspect underlying scatter plots

## 9) Practical Tips and Pitfalls
- Label units and transformations (e.g., log scale)
- Use consistent color palettes; ensure accessibility (colorblind-friendly)
- Don’t truncate axes to exaggerate differences (unless justified)
- Check sample sizes; small n can produce misleading shapes
- For skewed data, consider log or square-root transforms

## 10) Python Cookbook

### Setup
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set(style='whitegrid', context='notebook', palette='deep')
np.random.seed(42)

# Example dataset
n = 300
normal = np.random.normal(50, 10, n)
right_skew = np.random.gamma(shape=2.0, scale=8.0, size=n)
category = np.random.choice(['A', 'B', 'C'], size=n, p=[0.4, 0.4, 0.2])
value_x = normal
value_y = 0.6 * normal + np.random.normal(0, 7, n)

df = pd.DataFrame({'x': value_x, 'y': value_y, 'group': category, 'skewed': right_skew})
```

### Histograms and KDE
```python
fig, ax = plt.subplots(1, 2, figsize=(12, 4))

sns.histplot(df['x'], bins=20, kde=True, ax=ax[0])
ax[0].set_title('Histogram + KDE (x)')
ax[0].set_xlabel('x')

sns.kdeplot(df['skewed'], fill=True, ax=ax[1])
ax[1].set_title('Density Plot (Skewed)')
ax[1].set_xlabel('skewed')

plt.tight_layout(); plt.show()
```

### Box Plots and Violin Plots
```python
fig, ax = plt.subplots(1, 2, figsize=(12, 4))

sns.boxplot(x='group', y='x', data=df, ax=ax[0])
ax[0].set_title('Box Plot by Group')

sns.violinplot(x='group', y='x', data=df, inner='quartile', ax=ax[1])
ax[1].set_title('Violin Plot by Group (with Quartiles)')

plt.tight_layout(); plt.show()
```

### Bar Chart (Counts) and Proportions
```python
fig, ax = plt.subplots(1, 2, figsize=(12, 4))

# Counts
sns.countplot(x='group', data=df, ax=ax[0])
ax[0].set_title('Category Counts')

# Proportions
props = df['group'].value_counts(normalize=True).reset_index()
props.columns = ['group', 'proportion']
sns.barplot(x='group', y='proportion', data=props, ax=ax[1])
ax[1].set_ylim(0, 1)
ax[1].set_title('Category Proportions')

plt.tight_layout(); plt.show()
```

### Scatter with Regression Line and Facets
```python
sns.lmplot(x='x', y='y', hue='group', data=df, height=5, aspect=1.2)
plt.title('Scatter with Regression by Group'); plt.show()

# Facet by group
g = sns.FacetGrid(df, col='group', height=3, aspect=1)
g.map_dataframe(sns.scatterplot, x='x', y='y', alpha=0.7)
g.map_dataframe(sns.regplot, x='x', y='y', scatter=False, truncate=False)
g.set_titles(col_template='Group {col_name}')
plt.show()
```

### Line Plot and Rolling Mean
```python
# Create a simple time series
ts = pd.Series(df['x']).rolling(3, min_periods=1).mean()
plt.figure(figsize=(10, 4))
plt.plot(df.index, df['x'], alpha=0.4, label='x')
plt.plot(df.index, ts, color='red', label='Rolling Mean (window=3)')
plt.title('Line Plot with Rolling Mean')
plt.xlabel('Index'); plt.ylabel('x')
plt.legend(); plt.tight_layout(); plt.show()
```

### Pair Plot and Correlation Heatmap
```python
# Pair Plot
sns.pairplot(df[['x', 'y', 'skewed']])
plt.suptitle('Pair Plot', y=1.02)
plt.show()

# Correlation Heatmap
plt.figure(figsize=(5, 4))
corr = df[['x', 'y', 'skewed']].corr()
sns.heatmap(corr, annot=True, cmap='coolwarm', vmin=-1, vmax=1)
plt.title('Correlation Heatmap')
plt.tight_layout(); plt.show()
```

---
Navigation:
- Continue to [covariance_correlation.md](covariance_correlation.md) for relationships between variables
- Refer back to [percentiles_quartiles.md](percentiles_quartiles.md) for positional summaries
- See [pitfalls_best_practices.md](pitfalls_best_practices.md) for do’s and don’ts
- Explore [practical_applications.md](practical_applications.md) for end-to-end EDA workflows
