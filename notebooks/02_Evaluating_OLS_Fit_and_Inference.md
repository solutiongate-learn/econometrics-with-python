# Notebook 02: Evaluating OLS Fit and Inference

**Building on Notebook 01**

In Notebook 01, we estimated the import function for Trinidad and Tobago using OLS. In this notebook, we focus on **evaluating** how good that model is and conducting proper statistical inference.

## Learning Objectives

By the end of this notebook, you will be able to:

- Calculate and interpret $R^2$ and Adjusted $R^2$
- Interpret standard errors, t-statistics, and p-values
- Construct and interpret confidence intervals for coefficients
- Perform t-tests for individual coefficients
- Perform F-tests for joint significance
- Report regression results professionally

## 1. Quick Recap: The Import Function Model

We continue with the model from Notebook 01:

$$
M_t = \beta_1 + \beta_2 Y_t + \beta_3 \frac{p_m}{p_d} + u_t
$$

We will reload the data and re-estimate the model so this notebook remains self-contained.

```python
url = "https://raw.githubusercontent.com/solutiongate-learn/econometrics-with-python/main/data/trinidad_tobago_core.csv"
df = pd.read_csv(url)

y = df['IMPORTS']
X = sm.add_constant(df[['INCOME', 'RATIO']])

model = sm.OLS(y, X).fit()
print(model.summary())
```

## 2. Goodness of Fit

### R-squared ($R^2$)

Measures the proportion of variation in the dependent variable explained by the model.

```python
print("R-squared:", model.rsquared)
print("Adjusted R-squared:", model.rsquared_adj)
```

**Interpretation**: How much of the variation in imports is explained by income and relative prices?

### Adjusted R-squared

Penalizes the model for adding more variables. Useful when comparing models with different numbers of regressors.

## 3. Inference on Individual Coefficients

### Standard Errors, t-statistics, and p-values

```python
print(model.summary().tables[1])
```

- **Std. Error**: Measures precision of the coefficient estimate
- **t-statistic**: Tests $H_0: \beta_j = 0$
- **p-value**: Probability of observing the t-statistic if $H_0$ is true

### Confidence Intervals

```python
conf_int = model.conf_int(alpha=0.05)
print(conf_int)
```

## 4. Testing Joint Significance (F-test)

Tests whether **all slope coefficients are jointly zero**.

```python
print("F-statistic:", model.fvalue)
print("Prob (F-statistic):", model.f_pvalue)
```

**Null Hypothesis**: $\beta_2 = \beta_3 = 0$

## 5. Reporting Regression Results

A good regression table should include:

- Coefficient estimates
- Standard errors (in parentheses)
- t-statistics or p-values
- $R^2$, Adjusted $R^2$, F-statistic
- Number of observations

`statsmodels` summary provides most of this information.

## 6. Economic Evaluation

Statistical significance ≠ Economic significance.

Key questions to ask:
- Is the magnitude of the coefficient reasonable?
- Does the sign match economic theory?
- How large is the effect in practical terms?

## Exercises

1. Interpret the p-value of the coefficient on `RATIO`.
2. Construct a 99% confidence interval for the income coefficient.
3. Compare $R^2$ and Adjusted $R^2$. When would they differ significantly?

---

**Next:** Notebook 03 – Multicollinearity, Misspecification & Dummy Variables