# Notebook 11: Specification and Diagnostic Tests

## Learning Objectives

By the end of this notebook, you will be able to:

- Apply key specification tests to validate model assumptions
- Detect functional form misspecification (RESET)
- Test for normality of residuals (Jarque-Bera)
- Check for serial correlation (Ljung-Box, Breusch-Godfrey)
- Test for heteroscedasticity (White test)
- Detect structural breaks (Chow test)

## 1. Why Specification Testing Matters

Even if coefficients look significant, a model can be misspecified. Diagnostic testing helps ensure the model is reliable.

## 2. Key Diagnostic Tests

### Ramsey RESET Test (Functional Form)
```python
reset = sm.stats.diagnostic.linear_reset(model, power=2)
```

### Jarque-Bera Test (Normality)
```python
jb = sm.stats.jarque_bera(model.resid)
```

### Ljung-Box Test (Serial Correlation)
```python
lb = sm.stats.acorr_ljungbox(model.resid, lags=[10], return_df=True)
```

### White Test (Heteroscedasticity)
```python
white = sm.stats.diagnostic.het_white(model.resid, model.model.exog)
```

### Chow Test (Structural Break)
```python
# Requires splitting the sample
```

## 3. Practical Workflow

1. Estimate the model
2. Run diagnostic tests
3. If tests fail, consider respecification (add variables, change functional form, use robust methods)
4. Re-test

## 4. Key Takeaways

- Never rely only on coefficient significance
- Diagnostic testing should be routine
- Failed tests often point to better model specifications
- Combine multiple tests for robust conclusions

## Exercises

1. Run a full set of diagnostic tests on the import model.
2. Interpret the results of the RESET and Jarque-Bera tests.
3. What action would you take if the Chow test indicates a structural break?

---

**Next:** We can add more advanced or specialized notebooks as needed.