# Notebook 03: Multicollinearity, Misspecification & Dummy Variables

## Learning Objectives

By the end of this notebook, you will be able to:

- Detect multicollinearity and understand its consequences
- Use VIF and Condition Number to diagnose multicollinearity
- Identify model misspecification
- Apply and interpret dummy variables
- Use the Ramsey RESET test for functional form misspecification

## 1. Multicollinearity

### The Problem

Multicollinearity occurs when independent variables are highly correlated. It does **not** bias coefficients but makes them **imprecise** (large standard errors).

### Detection

**Variance Inflation Factor (VIF)**

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

vif = pd.DataFrame()
vif["Variable"] = X.columns
vif["VIF"] = [variance_inflation_factor(X.values, i) for i in range(len(X.columns))]
print(vif)
```

**Rules of thumb**:
- VIF > 5 or 10 → Potential multicollinearity problem
- Condition Number > 30 → Severe multicollinearity

### Consequences & Solutions

- Coefficients have large standard errors
- Individual t-tests may be insignificant even if the model is good
- Solutions: Drop one variable, combine variables, or accept it if prediction is the goal

## 2. Model Misspecification

### Ramsey RESET Test

Tests for omitted variables or incorrect functional form.

```python
reset_test = sm.stats.diagnostic.linear_reset(model, power=2)
print(reset_test)
```

## 3. Dummy Variables

Dummy variables allow inclusion of categorical information.

**Interpretation**:
- Coefficient on dummy = difference in intercept between groups
- Interaction term = difference in slope between groups

```python
model_dummy = smf.ols('IMPORTS ~ INCOME + RATIO + C(HighIncome)', data=df).fit()
```

## 4. Key Takeaways

- Always check VIF when you have multiple regressors
- Multicollinearity affects precision, not bias
- Dummy variables are powerful but need careful interpretation
- Use RESET test to check functional form

## Exercises

1. Calculate VIF for the import model. Is multicollinearity present?
2. Add a dummy variable and interpret its coefficient.
3. Run the RESET test. What does the result suggest about the model?

---

**Next:** Notebook 04 – Heteroscedasticity and Autocorrelation