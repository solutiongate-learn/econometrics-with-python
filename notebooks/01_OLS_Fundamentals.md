# Notebook 01: OLS Fundamentals

**The General Linear Regression Model**

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand the structure of the General Linear Regression Model
- Derive and apply Ordinary Least Squares (OLS) estimation (both conceptually and in code)
- Use `statsmodels` to estimate and interpret regression models
- Interpret regression coefficients in an economic context
- Replicate and extend the import function example from Chapter 1
- Perform basic diagnostic checks on residuals

## 1. Introduction

This notebook introduces the foundation of classical econometrics: the **General Linear Regression Model** and **Ordinary Least Squares (OLS)**.

We will use the **import function** from the book as our main running example:

$$
M_t = \beta_1 + \beta_2 Y_t + \beta_3 \left( \frac{p_m}{p_d} \right) + u_t
$$

Where:
- $M_t$ = Real imports
- $Y_t$ = Real income
- $p_m / p_d$ = Relative price of imports to domestic goods

## 2. The General Linear Regression Model

In matrix notation:

$$
y = X\beta + u$$

**Key Classical Assumptions:**

1. Linearity in parameters
2. $E(u) = 0$
3. No perfect multicollinearity
4. Homoscedasticity and no autocorrelation (for efficiency)
5. Exogeneity (for unbiasedness)

## 3. Ordinary Least Squares (OLS)

OLS minimizes the sum of squared residuals:

$$
\hat{\beta} = (X'X)^{-1}X'y
$$

This estimator is **BLUE** (Best Linear Unbiased Estimator) under the classical assumptions (Gauss-Markov Theorem).

## 4. Practical Implementation in Python

```python
import statsmodels.api as sm
import pandas as pd

url = "https://raw.githubusercontent.com/solutiongate-learn/econometrics-with-python/main/data/trinidad_tobago_core.csv"
df = pd.read_csv(url)

y = df['IMPORTS']
X = df[['INCOME', 'RATIO']]
X = sm.add_constant(X)                    # Add intercept

model = sm.OLS(y, X).fit()
print(model.summary())
```

## 5. Interpreting the Results

Focus on these key elements:

- **Coefficients**: Economic meaning (e.g., marginal propensity to import)
- **Standard Errors & t-stats**: Precision and significance
- **p-values**: Probability of observing the result if null is true
- **R-squared**: Proportion of variance explained
- **F-statistic**: Overall model significance

**Economic Interpretation Example**:
- A coefficient of 0.38 on INCOME means that, on average, a $1 million increase in income is associated with a $0.38 million increase in imports (holding relative prices constant).

## 6. Basic Residual Diagnostics

```python
import matplotlib.pyplot as plt

import seaborn as sns

sns.residplot(x=model.fittedvalues, y=model.resid, lowess=True)
plt.title('Residuals vs Fitted')
plt.show()
```

## 7. Key Takeaways

- OLS is the workhorse of econometrics
- Always interpret coefficients in economic terms
- Check residual plots early
- Statistical significance ≠ economic importance
- The constant term often has limited economic meaning

## Exercises

1. Estimate the model without the `RATIO` variable. How does $R^2$ change?
2. Interpret the coefficient on `INCOME` in plain English.
3. Plot the residuals. Do you see any patterns?
4. What economic factors might be missing from this simple import model?

---

**Next Notebook:** `02_Evaluating_OLS_Fit_and_Inference.md`