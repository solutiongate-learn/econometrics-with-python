# Notebook 12: Maximum Likelihood Estimation and Testing Principles

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand the concept of Maximum Likelihood Estimation (MLE)
- Know the properties of MLEs (consistency, efficiency, asymptotic normality)
- Apply the three main testing frameworks: Wald, Likelihood Ratio (LR), and Lagrange Multiplier (LM)
- Choose the appropriate test in different situations

## 1. What is Maximum Likelihood Estimation?

MLE finds the parameter values that maximize the likelihood of observing the given data.

It is widely used in modern econometrics because of its desirable asymptotic properties.

## 2. Key Properties of MLE

- Consistent
- Asymptotically efficient
- Asymptotically normal
- Invariant to reparameterization

## 3. The Three Testing Principles

### Wald Test
Tests restrictions on parameters after estimation.

### Likelihood Ratio (LR) Test
Compares the fit of restricted vs unrestricted models.

### Lagrange Multiplier (LM) Test
Tests restrictions using only the restricted model (very useful for diagnostics).

```python
# Example using statsmodels
wald_test = model.wald_test('INCOME = 0')
print(wald_test)
```

## 4. When to Use Which Test?

- **Wald**: Easy to compute after estimation
- **LR**: Generally most powerful
- **LM**: Useful when the unrestricted model is hard to estimate

## 5. Key Takeaways

- MLE is the foundation of many modern econometric techniques
- The three testing principles are asymptotically equivalent
- Understanding these tests helps in model selection and diagnostic checking
- `statsmodels` and `linearmodels` provide convenient implementations

## Exercises

1. Estimate a model using MLE and perform a Wald test.
2. Compare LR and Wald test results on the same restriction.
3. Discuss situations where the LM test would be preferred.

---

**Next:** We can continue with additional specialized notebooks.