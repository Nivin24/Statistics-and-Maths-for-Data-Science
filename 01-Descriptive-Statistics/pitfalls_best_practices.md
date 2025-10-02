# Common Pitfalls and Best Practices in Descriptive Statistics

Mastery of descriptive statistics means not just knowing how to compute them, but also understanding where mistakes happen and how to avoid them. Here’s your guide to prevent errors and ensure reliable analysis.

---

## Common Pitfalls

**1. Over-reliance on the Mean**
- The mean (average) is sensitive to outliers and skewed data.
- *Mistake:* Using mean for highly skewed distributions (e.g., income, wait times).
- *Solution:* Use median and mode alongside mean.

**2. Ignoring Outliers**
- Outliers can distort summary statistics and model results.
- *Mistake:* Failing to visualize or treat outliers.
- *Solution:* Always plot data (boxplot, scatterplot) and decide how to handle outliers using domain knowledge.

**3. Confusing Correlation with Causation**
- Correlation indicates association, not causal relationships.
- *Mistake:* Assuming “A correlates with B” means “A causes B.”
- *Solution:* Use caution; seek supporting evidence for causation.

**4. Misinterpreting Standard Deviation and Standard Error**
- Standard deviation measures spread among values; standard error measures accuracy of sample mean.
- *Mistake:* Reporting SD when SE is needed (or vice versa).
- *Solution:* Know the difference and use the correct metric.

**5. Ignoring Data Type**
- Some statistics are only meaningful for specific data types (e.g., mean for continuous data).
- *Mistake:* Calculating a mean on categorical labels.
- *Solution:* Match summary measures to variable type.

**6. Overgeneralizing from Small Samples**
- Small samples may not represent the true population.
- *Mistake:* Making strong claims based on limited data.
- *Solution:* Report sample size; interpret findings with caution.

**7. Not Visualizing Data**
- Summary values can hide patterns, trends, and errors.
- *Mistake:* Relying entirely on statistics.
- *Solution:* Always accompany summary statistics with visualizations.

**8. Forgetting Context and Domain Knowledge**
- Statistics without domain context can be misleading.
- *Mistake:* Interpreting data without understanding its source, meaning, or limitations.
- *Solution:* Incorporate context and consult domain experts as needed.

---

## Best Practices

**1. Use Multiple Measures**
- Report mean, median, mode, SD, IQR, and range when summarizing data.
- Compare and discuss differences.

**2. Always Visualize Data**
- Use appropriate plots: histograms, boxplots, scatterplots, bar charts, etc.

**3. Document Steps and Decisions**
- Record data cleaning, transformation, and rationale for chosen methods.

**4. State Limitations**
- Clearly mention sample size, missing values, and any assumptions.

**5. Match Statistic to Data Type**
- For categorical: use mode and frequency counts.
- For continuous: use mean, median, SD, IQR.

**6. Validate Findings**
- Review results with domain stakeholders or experts.
- Cross-check with multiple methods when possible.

**7. Handle Missing Data Thoughtfully**
- Decide whether to impute, remove, or flag missing data.
- Report how missingness was addressed.

---

## Quick Reference

- **Mean:** Sensitive to outliers/skew  
- **Median:** Robust to outliers/skew  
- **Mode:** Best for categories  
- **SD/IQR:** Show spread/variability  
- **Visualize First:** Always check the picture and summary numbers

---

## Summary

The most reliable descriptive statistics come from a deep understanding of the data, its context, and careful, documented analysis. Combining visualizations with multiple summary measures and clear best practices is essential for trustworthy insights.

---

## Further Reading

- “Data Science for Business” – Provost & Fawcett
- “Python for Data Analysis” – Wes McKinney
- [Good statistical practices – Wikipedia](https://en.wikipedia.org/wiki/Good_statistical_practice)
