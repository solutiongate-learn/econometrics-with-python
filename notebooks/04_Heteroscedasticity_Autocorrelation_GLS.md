# Notebook 04: Heteroscedasticity, Autocorrelation & GLS

## Learning Objectives

By the end of this notebook, you will be able to:

- Detect heteroscedasticity and autocorrelation
- Understand the consequences of these violations
- Apply modern robust standard errors (HC and HAC)
- Implement Feasible Generalized Least Squares when appropriate
- Choose the right remedy for different situations

## 1. Why Violations Matter

When heteroscedasticity or autocorrelation is present:
- OLS remains **unbiased** but is no longer **efficient**
- Standard errors are biased → invalid t-tests and confidence intervals
- Inference becomes unreliable

## 2. Heteroscedasticity

### Detection

**Breusch-Pagan / Koenker Test**
```python
from statsmodels.stats.diagnostic import het_breuschpagan

bp_test = het_breuschpagan(model.resid, model.model.exog)
print("Breusch-Pagan p-value:", bp_test[1])
```

**White Test**

### Remedies

1. **Robust Standard Errors** (Recommended first approach)
```python
model_robust = model.get_robustcov_results(cov_type='HC3')
```

2. **Weighted / Feasible GLS**

## 3. Autocorrelation

### Detection

**Durbin-Watson Test**
```python
print("Durbin-Watson:", model.dw)
```

**Breusch-Godfrey Test** (better for higher lags)

### Remedies

- **HAC Standard Errors** (Newey-West)
```python
model_hac = model.get_robustcov_results(cov_type='HAC', maxlags=4)
```
- Cochrane-Orcutt / Prais-Winsten

## 4. Practical Decision Framework

| Problem                    | Recommended Solution          |
|---------------------------|-------------------------------|
| Heteroscedasticity only   | HC3 robust SE                 |
| Autocorrelation           | HAC (Newey-West)              |
| Both                      | HAC                           |
| Severe violations         | Consider FGLS or model respecification |

## 5. Key Takeaways

- Robust standard errors are often the simplest and safest solution
- They correct inference, not the coefficients themselves
- Always diagnose first, then choose the remedy
- Report which type of robust SE you used

## Exercises

1. Test the import model for heteroscedasticity.
2. Apply HC3 robust standard errors and compare results.
3. Run the Durbin-Watson test. Is there autocorrelation?

---

**Next:** Notebook 05 – Dynamic Models