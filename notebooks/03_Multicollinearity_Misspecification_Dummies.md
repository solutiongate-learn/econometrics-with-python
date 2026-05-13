# Notebook 03: Multicollinearity, Misspecification & Dummy Variables

## Learning Objectives

By the end of this notebook, you will be able to:

- Detect multicollinearity using VIF and Condition Number
- Understand the consequences of multicollinearity
- Identify model misspecification
- Use and interpret dummy variables
- Apply Ramsey RESET test for functional form misspecification

## 1. Multicollinearity

### The Problem

Multicollinearity occurs when independent variables are highly correlated. It does not bias coefficients but makes them **imprecise** (high standard errors).

### Detection

```python
# Variance Inflation Factor (VIF)
from statsmodels.stats.outliers_influence import variance_inflation_factor

vif_data = pd.DataFrame()
vif_data["Variable"] = X.columns
vif_data["VIF"] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
print(vif_data)
```

**Rules of thumb**:
- VIF > 5 or 10 → Potential problem
- Condition Number > 30 → Severe multicollinearity

### Solutions

- Remove one of the correlated variables
- Combine variables (e.g., principal components)
- Collect more data
- Accept it if prediction is the goal (not inference)

## 2. Model Misspecification

### Types of Misspecification

- Omitted variable bias
- Wrong functional form
- Incorrect variable measurement

### Ramsey RESET Test

Tests for omitted variables or incorrect functional form.

```python
reset_test = sm.stats.diagnostic.linear_reset(model, power=2)
print(reset_test)
```

## 3. Dummy Variables

Dummy variables allow us to include categorical information.

### Interpretation

- Coefficient on dummy = difference in intercept between groups
- Interaction terms = difference in slopes

```python
# Example: Adding a dummy variable
model_with_dummy = smf.ols('IMPORTS ~ INCOME + RATIO + C(Period)', data=df).fit()
print(model_with_dummy.summary())
```

## 4. Key Takeaways from Chapter 3

- Multicollinearity affects precision, not unbiasedness
- Always check VIF when you have multiple regressors
- Dummy variables are powerful but require careful interpretation
- Specification testing (like RESET) should be part of your workflow

## Exercises

1. Calculate VIF for the import model. Is multicollinearity a concern?
2. Add a dummy variable to the model and interpret the coefficient.
3. Run the RESET test. What does the result suggest?

---

**Next:** Notebook 04 – Heteroscedasticity and Autocorrelation