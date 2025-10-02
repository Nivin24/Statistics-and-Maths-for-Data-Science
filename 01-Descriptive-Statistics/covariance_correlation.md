# Covariance and Correlation

Understanding how variables move together is vital in statistics, data science, and ML. This file explains covariance and correlation, their differences, calculations, interpretations, and practical usage.

---

## Covariance

**Definition:**  
Covariance measures the direction of the linear relationship between two variables.  
- Positive covariance: Variables increase together  
- Negative covariance: As one increases, the other decreases  
- Zero covariance: No linear relationship

**Formula:**  
\[
\mathrm{Cov}(X, Y) = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{n-1}
\]  
Where \(\bar{x}\) and \(\bar{y}\) are the means of X and Y.

**Example:**  
If exam score and study hours have a positive covariance, students who study more tend to score higher.

---

## Correlation

**Definition:**  
Correlation standardizes covariance, measuring both the strength and direction of the linear relationship. Value ranges from -1 to 1.  
- \(+1\): Perfect positive linear relationship  
- \(-1\): Perfect negative linear relationship  
- \(0\): No linear relationship

**Pearson’s Correlation coefficient (r) formula:**  
\[
r = \frac{\mathrm{Cov}(X, Y)}{\sigma_X \sigma_Y}
\]  
Where \(\sigma_X\) and \(\sigma_Y\) are standard deviations of X and Y.

**Interpretation:**  
- \(0 < |r| < 0.3\): Weak  
- \(0.3 \leq |r| < 0.7\): Moderate  
- \(|r| \geq 0.7\): Strong

---

### Example Calculation

Suppose we have:

| X | Y |
|---|---|
| 2 | 6 |
| 4 | 8 |
| 5 | 10|
| 6 | 12|

Calculate means, covariance, and correlation as per the above formulas.

---

### Pearson vs Spearman Correlation

- **Pearson**: Requires normality, captures linear relationships
- **Spearman**: Rank-based, useful for non-linear monotonic relationships

---

## Practical Usage in Data Science

- **Feature Selection:** Identify related variables
- **Multicollinearity:** Spot correlations between predictors in regression
- **EDA:** Understand relationships to guide further analysis
- **Time-Series:** Check autocorrelation and trends

---

## Pitfalls & Best Practices

- **Correlation ≠ Causation:** Just because two variables are correlated does not mean one causes the other.
- **Outliers:** They can strongly skew covariance and correlation.
- **Nonlinearity:** Pearson’s r only measures linear relationships.

---

## Python Quick Reference
```python
import pandas as pd

df[['feature1', 'feature2']].cov()
df[['feature1', 'feature2']].corr() # Pearson by default
df[['feature1', 'feature2']].corr(method='spearman') # Spearman
```

---

## References
- [Wikipedia: Covariance](https://en.wikipedia.org/wiki/Covariance)
- [Wikipedia: Correlation](https://en.wikipedia.org/wiki/Correlation_and_dependence)
- [Python: pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html)

