# Notebook 15: Robust Inference and Standard Errors

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand when and why to use robust standard errors
- Apply different types of robust covariance estimators
- Choose between HC, HAC, and clustered standard errors
- Improve the reliability of inference in the presence of violations

## 1. Why Robust Standard Errors?

Classical OLS standard errors assume homoscedasticity and no autocorrelation. When these assumptions are violated, inference can be misleading even if coefficients are unbiased.

Robust standard errors provide valid inference under weaker assumptions.

## 2. Types of Robust Standard Errors

### Heteroscedasticity-Consistent (HC)
- HC0, HC1, HC2, HC3
- HC3 is often recommended in practice

```python
model_robust = model.get_robustcov_results(cov_type='HC3')
```

### Heteroscedasticity and Autocorrelation Consistent (HAC)
- Newey-West estimator
- Useful for time series data

```python
model_hac = model.get_robustcov_results(cov_type='HAC', maxlags=4)
```

### Clustered Standard Errors
- Useful for panel or grouped data

## 3. Practical Guidance

| Situation                    | Recommended Approach          |
|-----------------------------|-------------------------------|
| Heteroscedasticity only     | HC3                           |
| Time series (autocorrelation) | HAC (Newey-West)            |
| Panel data                  | Clustered SE                  |
| Both hetero + auto          | HAC                           |

## 4. Key Takeaways

- Robust standard errors are often the easiest and safest default in applied work
- They do not fix biased coefficients — only inference
- Always report which type of robust SE you are using
- Combine with proper model specification

## Exercises

1. Re-estimate one of your models with HC3 robust standard errors.
2. Compare results with classical standard errors.
3. When would you prefer HAC over simple HC standard errors?

---

**This adds an important practical layer to inference.**