# Notebook 04: Heteroscedasticity, Autocorrelation & GLS

## Learning Objectives

By the end of this notebook, you will be able to:

- Detect heteroscedasticity using statistical tests
- Detect autocorrelation (serial correlation)
- Understand the consequences of violating classical assumptions
- Apply robust standard errors (HC and HAC)
- Implement Feasible Generalized Least Squares (GLS)

## 1. Why Do Violations Matter?

When heteroscedasticity or autocorrelation is present:

- OLS remains **unbiased** but is **no longer efficient**
- Standard errors are biased
- t-statistics and F-tests become unreliable
- Confidence intervals are incorrect

## 2. Heteroscedasticity

### Detection

**Breusch-Pagan / Koenker Test**
```python
from statsmodels.stats.diagnostic import het_breuschpagan

bp_test = het_breuschpagan(model.resid, model.model.exog)
print("Breusch-Pagan p-value:", bp_test[1])
```

**White Test**
```python
white_test = sm.stats.diagnostic.het_white(model.resid, model.model.exog)
```

### Remedies

1. **Robust Standard Errors** (Recommended in most cases)
```python
model_robust = model.get_robustcov_results(cov_type='HC3')
print(model_robust.summary())
```

2. **Weighted Least Squares / Feasible GLS**

## 3. Autocorrelation (Serial Correlation)

### Detection

**Durbin-Watson Test**
```python
print("Durbin-Watson statistic:", model.dw)
```

**Breusch-Godfrey Test** (Better for higher-order autocorrelation)
```python
bg_test = sm.stats.diagnostic.acorr_breusch_godfrey(model, nlags=2)
```

### Remedies

- Newey-West HAC standard errors
```python
model_hac = model.get_robustcov_results(cov_type='HAC', maxlags=2)
```
- Cochrane-Orcutt / Prais-Winsten (Feasible GLS)

## 4. Practical Recommendations

| Problem              | First Choice                  | Alternative             |
|----------------------|-------------------------------|-------------------------|
| Heteroscedasticity   | Robust SE (HC3)               | WLS / FGLS              |
| Autocorrelation      | HAC (Newey-West)              | Cochrane-Orcutt         |
| Both                 | HAC                           | Cluster-robust SE       |

## 5. Key Takeaways from Chapter 4

- Always test for heteroscedasticity and autocorrelation in time series data
- Robust standard errors are often the simplest and most robust solution
- GLS is more efficient when assumptions are correct, but robust SEs are safer in practice

## Exercises

1. Test the import model for heteroscedasticity using the Breusch-Pagan test.
2. Apply HC3 robust standard errors. How do the results change?
3. Run the Durbin-Watson test. Is there evidence of autocorrelation?

---

**Next:** Notebook 05 – Dynamic Models and Error Correction