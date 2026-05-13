# Notebook 06: Instrumental Variables and Endogeneity

## Learning Objectives

By the end of this notebook, you will be able to:

- Understand the problem of endogeneity and why OLS fails
- Grasp the concept of Instrumental Variables (IV)
- Implement Two-Stage Least Squares (2SLS)
- Test for endogeneity and weak instruments
- Interpret IV results correctly

## 1. The Problem of Endogeneity

OLS is biased and inconsistent when:

- There is correlation between regressors and the error term
- Common causes: Omitted variables, measurement error, simultaneity/reverse causality

## 2. Instrumental Variable (IV) Approach

An instrument must satisfy two conditions:

1. **Relevance**: Correlated with the endogenous regressor
2. **Exogeneity**: Not correlated with the error term

## 3. Two-Stage Least Squares (2SLS)

```python
from linearmodels.iv import IV2SLS

# Example syntax
iv_model = IV2SLS.from_formula('y ~ 1 + [x ~ z]', data=df).fit()
print(iv_model.summary)
```

Where `z` is the instrument for the endogenous variable `x`.

## 4. Testing for Endogeneity

**Hausman Test** (comparing OLS vs IV)

**Weak Instrument Tests**

## 5. Key Takeaways from Chapter 6

- IV/2SLS is one of the most important tools when endogeneity is suspected
- Finding good instruments is often the hardest part
- Always report first-stage results and diagnostics
- IV estimates are usually less precise than OLS

## Exercises

1. Identify potential endogenous variables in an economic model.
2. Discuss what would make a good instrument.
3. Estimate a simple IV model and compare with OLS.

---

**Next:** Notebook 07 – Simultaneous Equation Systems