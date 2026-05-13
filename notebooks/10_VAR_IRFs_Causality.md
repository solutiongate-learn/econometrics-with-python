# Notebook 10: VAR, Impulse Responses & Causality

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand and estimate Vector Autoregression (VAR) models
- Select optimal lag length
- Generate and interpret Impulse Response Functions (IRFs)
- Perform Forecast Error Variance Decomposition
- Conduct Granger Causality tests

## 1. What is a VAR Model?

A VAR model treats all variables as endogenous. Each variable is modeled as a function of its own lags and the lags of all other variables in the system.

This is very useful for understanding dynamic interactions between macroeconomic variables.

## 2. Estimating a VAR

```python
from statsmodels.tsa.vector_ar.var_model import VAR

model = VAR(df[['IMPORTS', 'INCOME']])
results = model.fit(maxlags=4, ic='aic')
print(results.summary())
```

## 3. Lag Length Selection

Use information criteria (AIC, BIC, HQIC) or sequential likelihood ratio tests.

## 4. Impulse Response Functions (IRFs)

IRFs show how a shock to one variable affects other variables over time.

```python
irf = results.irf(10)  # 10 periods
irf.plot()
plt.show()
```

## 5. Forecast Error Variance Decomposition (FEVD)

Shows how much of the forecast error variance of each variable is explained by shocks to other variables.

```python
fevd = results.fevd(10)
fevd.plot()
```

## 6. Granger Causality

Tests whether past values of one variable help predict another variable.

```python
granger = results.test_causality('IMPORTS', 'INCOME', kind='f')
print(granger.summary())
```

## 7. Key Takeaways

- VAR is excellent for multivariate dynamic analysis
- IRFs and FEVD provide rich economic insights
- Granger causality is about predictability, not true causation
- Always ensure variables are stationary (or cointegrated) before estimating VAR

## Exercises

1. Estimate a VAR with 3 variables and select lag length.
2. Plot and interpret impulse responses.
3. Perform Granger causality tests in both directions.

---

**Next:** Further topics or review of existing notebooks.