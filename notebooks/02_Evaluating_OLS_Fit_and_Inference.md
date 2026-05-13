# Notebook 02: Evaluating OLS Fit and Inference

**Building on Notebook 01**

In Notebook 01, we estimated the import function. Now we learn how to properly **evaluate** the model and conduct statistical inference.

## Learning Objectives

By the end of this notebook, you will be able to:

- Calculate and interpret $R^2$ and Adjusted $R^2$
- Interpret standard errors, t-statistics, and p-values
- Construct and interpret confidence intervals
- Perform hypothesis tests on individual coefficients (t-tests)
- Perform joint hypothesis tests (F-test)
- Report regression results professionally
- Combine statistical and economic evaluation

## 1. Recap: The Import Function Model

We continue with:

$$
M_t = \beta_1 + \beta_2 Y_t + \beta_3 \left( \frac{p_m}{p_d} \right) + u_t
$$

We reload the data and re-estimate so this notebook is self-contained.

```python
url = "https://raw.githubusercontent.com/solutiongate-learn/econometrics-with-python/main/data/trinidad_tobago_core.csv"
df = pd.read_csv(url)

y = df['IMPORTS']
X = sm.add_constant(df[['INCOME', 'RATIO']])
model = sm.OLS(y, X).fit()
```

## 2. Goodness of Fit

### R-squared ($R^2$)

Proportion of variation in the dependent variable explained by the model.

```python
print("R-squared:", model.rsquared)
print("Adjusted R-squared:", model.rsquared_adj)
```

**Interpretation**: How much of the variation in imports can be explained by income and relative prices?

### Adjusted R-squared

Penalizes the addition of extra variables. Better for comparing models.

## 3. Inference on Individual Coefficients

### t-test

Tests $H_0: \beta_j = 0$.

Key outputs:
- Coefficient
- Standard Error
- t-statistic
- p-value

```python
print(model.summary().tables[1])
```

### Confidence Intervals

```python
print(model.conf_int(alpha=0.05))
```

## 4. Joint Hypothesis Testing (F-test)

Tests whether a group of coefficients are jointly zero.

```python
print("F-statistic:", model.fvalue)
print("p-value:", model.f_pvalue)
```

## 5. Reporting Regression Results

A good table should include:
- Coefficients + Standard Errors
- t-stats or p-values
- $R^2$, Adjusted $R^2$, F-statistic
- Number of observations

## 6. Economic vs Statistical Evaluation

- Is the coefficient **statistically significant**?
- Is the magnitude **economically meaningful**?
- Does the sign match theory?

## 7. Key Takeaways

- $R^2$ measures fit, but Adjusted $R^2$ is better for model comparison
- Always report confidence intervals or standard errors
- Statistical significance does not imply economic importance
- The F-test checks overall model relevance

## Exercises

1. Interpret the p-value on the `RATIO` variable.
2. Construct a 99% confidence interval for the income coefficient.
3. Compare $R^2$ and Adjusted $R^2$. When do they differ most?
4. Perform an F-test that both slope coefficients are zero.

---

**Next:** Notebook 03 – Multicollinearity, Misspecification & Dummy Variables