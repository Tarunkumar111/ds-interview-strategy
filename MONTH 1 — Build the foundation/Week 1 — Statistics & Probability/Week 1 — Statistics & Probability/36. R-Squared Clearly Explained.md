# R-squared, Clearly Explained!!!

## 1. What is R-squared?

**R-squared (\(R^2\))** is a measure used in regression to describe **how much of the variation in the dependent variable is explained by the regression model**.

It is also called the **coefficient of determination**.

For example, suppose we're predicting house prices using:

* house size
* number of bedrooms
* location
* age of house

If:

$$
R^2=0.80
$$

we commonly say:

> The model explains **80% of the variation in house prices** in the data used for the calculation.

The remaining 20% is variation not explained by the model.

---

# 2. The Core Intuition

Imagine the actual house prices look like this:

```text
Actual values
   •       •
      •  •
 •       •    •
    •       •
       •
```

Our model tries to predict those values.

If predictions are very close to actual values:

```text
Actual:      • • • • • •
Prediction:  × × × × × ×
             ↑
        close together
```

Then \(R^2\) is high.

If predictions are poor:

```text
Actual:      •       •
       •          •
   •          •
            •       •

Prediction:     ×
         ×
              ×
    ×
                    ×
```

Then \(R^2\) is low.

### Mental model

> **\(R^2\) asks: "How much better is my model at explaining the variation compared with simply predicting the mean?"**

---

# 3. Why Do We Need a Baseline?

Suppose we're predicting employee salaries.

The simplest possible prediction is:

> Predict everyone's salary as the average salary.

That's our **baseline model**.

Now suppose a regression model uses:

* experience
* education
* job level
* location

and produces much better predictions.

\(R^2\) measures the improvement in explaining variation relative to that mean-based baseline.

---

# 4. The Formula

The standard formula is:

$$
\boxed{
R^2=1-\frac{SS_{\text{res}}}{SS_{\text{tot}}}
}
$$

where:

### Total Sum of Squares

$$
SS_{\text{tot}}=\sum_{i=1}^{n}(y_i-\bar y)^2
$$

This measures the **total variation in the observed values around their mean**.

### Residual Sum of Squares

$$
SS_{\text{res}}=\sum_{i=1}^{n}(y_i-\hat y_i)^2
$$

This measures the **variation left unexplained by the model**.

Therefore:

$$
\boxed{
R^2=1-\frac{\text{Unexplained Variation}}
{\text{Total Variation}}
}
$$

---

# 5. The Most Important Formula to Remember

You can think of it as:

$$
\boxed{
R^2=
\frac{\text{Explained Variation}}
{\text{Total Variation}}
}
$$

because:

$$
\text{Total Variation}
=
\text{Explained Variation}
+
\text{Unexplained Variation}
$$

So:

```text
Total variation
████████████████████

Explained
████████████████

Unexplained
                ████
```

If 80% is explained:

$$
R^2=0.80
$$

---

# 6. Simple Example

Suppose actual values are:

$$
y=[10,20,30,40,50]
$$

Mean:

$$
\bar y=30
$$

Suppose our model predicts:

$$
\hat y=[12,22,28,38,48]
$$

The predictions are relatively close to the actual values.

Suppose the calculations give:

$$
SS_{\text{tot}}=1000
$$

and:

$$
SS_{\text{res}}=100
$$

Then:

$$
R^2=1-\frac{100}{1000}
$$

$$
R^2=0.90
$$

Therefore:

$$
\boxed{R^2=0.90}
$$

We can say:

> The model explains 90% of the variation in the observed response values, relative to the mean-only baseline.

---

# 7. What Does \(R^2=0\) Mean?

If:

$$
R^2=0
$$

the model provides no improvement over predicting the mean, under the usual regression setup with an intercept.

In other words:

```text
Model prediction
       ↓
      Mean
       ↓
No additional variation explained
```

Example:

Average salary = ₹50,000.

If our model predicts approximately ₹50,000 for everyone, it isn't explaining differences in salaries.

---

# 8. What Does \(R^2=1\) Mean?

If:

$$
R^2=1
$$

the model perfectly explains the variation in the observed response.

That means:

$$
SS_{\text{res}}=0
$$

and therefore:

$$
R^2=1-\frac{0}{SS_{\text{tot}}}=1
$$

Every prediction exactly matches the observed value.

```text
Actual:      • • • • •
Prediction:  × × × × ×
             ↓
         Perfect fit
```

---

# 9. Can \(R^2\) Be Negative?

**Yes, depending on the model and how predictions are evaluated.**

For ordinary least-squares regression **with an intercept on the same training data**, \(R^2\) is typically between:

$$
0\le R^2\le1
$$

But \(R^2\) can be negative when evaluated on new/test data or for certain models, especially when the model performs worse than the mean-only baseline.

For example:

$$
R^2=-0.20
$$

means the model's squared prediction errors are worse than simply predicting the mean.

### Important

A negative \(R^2\) does **not** mean "negative percentage of variation explained."

It means:

> The model performs worse than the mean baseline under the \(R^2\) criterion.

---

# 10. \(R^2\) and Correlation

For **simple linear regression with one predictor and an intercept**:

$$
\boxed{R^2=r^2}
$$

where \(r\) is the Pearson correlation coefficient.

For example:

$$
r=0.8
$$

Then:

$$
R^2=(0.8)^2=0.64
$$

So:

$$
\boxed{R^2=0.64}
$$

The model explains 64% of the variation in \(Y\).

---

## What if \(r=-0.8\)?

$$
r^2=(-0.8)^2=0.64
$$

So:

$$
R^2=0.64
$$

Notice something important:

> \(R^2\) doesn't tell you the **direction** of the relationship.

Correlation does:

$$
r=+0.8 \quad\text{vs}\quad r=-0.8
$$

But:

$$
R^2=0.64
$$

for both.

---

# 11. \(R^2\) vs Correlation

|                          | Correlation \(r\)  | R-squared \(R^2\)                                |
| ------------------------ | ------------------ | ------------------------------------------------ |
| Measures                 | Linear association | Variation explained by regression                |
| Range                    | \([-1,+1]\)        | Usually \([0,1]\) on training OLS with intercept |
| Direction?               | Yes                | No                                               |
| Units                    | None               | None                                             |
| Can be negative?         | Yes                | Yes in some out-of-sample/model settings         |
| Simple linear regression | —                  | \(R^2=r^2\)                                      |

### Mental model

> **Correlation tells you direction + strength of linear association.**

> **R-squared tells you how much variation the regression explains relative to a mean baseline.**

---

# 12. High \(R^2\) Does NOT Mean the Model Is Good

This is extremely important.

Suppose:

$$
R^2=0.95
$$

It may look impressive.

But a high \(R^2\) doesn't automatically mean:

* the model is causal
* the model generalizes well
* the model is useful
* the model has no bias
* the model has no overfitting
* the predictors are meaningful

For example, a model can have a very high training \(R^2\) because it **overfits** the training data.

---

# 13. Training \(R^2\) vs Test \(R^2\)

Suppose:

### Training data

$$
R^2=0.95
$$

### Test data

$$
R^2=0.40
$$

That's a warning sign.

The model explains 95% of the variation in the training data but only 40% on unseen data.

This could indicate **overfitting**.

```text
Training
Model learns:
████████████████████
R² = 0.95

Test
Performance:
████████
R² = 0.40
```

For machine learning, **out-of-sample performance is usually much more important** than training \(R^2\).

---

# 14. High \(R^2\) vs Low \(R^2\)

### High \(R^2\)

$$
R^2\approx1
$$

The model explains a large fraction of variation.

### Low \(R^2\)

$$
R^2\approx0
$$

The model explains relatively little variation compared with the mean baseline.

But whether an \(R^2\) is "good" depends heavily on the domain.

For some physical systems:

$$
R^2=0.95
$$

might be expected.

For some social-science problems:

$$
R^2=0.30
$$

could still be useful.

There is **no universal threshold** such as:

> "R² above 0.7 is good."

---

# 15. R-squared Does NOT Measure Prediction Error Directly

Suppose two models have:

$$
R^2=0.80
$$

That doesn't tell you directly whether their prediction errors are small in business terms.

You should also consider metrics such as:

* MAE
* MSE
* RMSE
* MAPE, where appropriate

For example:

$$
R^2=0.80
$$

could still correspond to an RMSE of ₹50,000, which might be unacceptable for a particular business problem.

### Important

> \(R^2\) describes explained variation; it is not a direct measure of prediction error magnitude.

---

# 16. R-squared and Residuals

Remember:

$$
\text{Residual}=y-\hat y
$$

The residual tells us how far a prediction is from the actual value.

$$
SS_{\text{res}}=\sum(y_i-\hat y_i)^2
$$

If residuals are small:

$$
SS_{\text{res}}\downarrow
$$

Then:

$$
R^2\uparrow
$$

So:

```text
Better predictions
       ↓
Smaller residuals
       ↓
Smaller residual sum of squares
       ↓
Higher R²
```

---

# 17. R-squared and Adding Predictors

Here's an important property of ordinary training \(R^2\):

> Adding another predictor to an OLS model cannot decrease the training \(R^2\).

Even if the new predictor is useless, the model can usually fit the training data at least as well.

For example:

```text
Model 1:
Experience → Salary
R² = 0.60

Model 2:
Experience + Age → Salary
R² = 0.65

Model 3:
Experience + Age + Random_Number → Salary
R² = 0.66
```

That doesn't mean the random number is genuinely useful.

It could simply exploit noise.

This is one reason we sometimes use **Adjusted R-squared**.

---

# 18. Adjusted R-squared

Adjusted \(R^2\) penalizes the model for adding unnecessary predictors.

A common formula is:

$$
\boxed{
\text{Adjusted }R^2
=
1-(1-R^2)\frac{n-1}{n-p-1}
}
$$

where:

* \(n\) = number of observations
* \(p\) = number of predictors

Unlike ordinary \(R^2\), adjusted \(R^2\) can **decrease** when a predictor doesn't provide enough additional explanatory value.

### Mental model

```text
R²
↓
Rewards better fit

Adjusted R²
↓
Rewards better fit
+
Penalizes unnecessary predictors
```

---

# 19. R-squared Does Not Mean Causation

Suppose:

$$
R^2=0.90
$$

between ice cream sales and swimming accidents.

That doesn't mean:

> Ice cream causes swimming accidents.

A third variable—such as **hot weather**—could influence both.

```text
        Hot Weather
        ↙         ↘
Ice Cream       Swimming
 Sales           Accidents
```

So:

$$
\boxed{\text{High }R^2\neq\text{Causation}}
$$

---

# 20. R-squared Can Be Misleading

A high \(R^2\) can occur because of:

* Confounding variables
* Trends over time
* Overfitting
* Data leakage
* Spurious relationships
* Inappropriate model specification

Therefore, never evaluate a regression model using \(R^2\) alone.

Look at:

* residual plots
* test-set performance
* RMSE/MAE
* coefficient uncertainty
* model assumptions
* feature leakage
* domain relevance

---

# 21. Example: House Price Prediction

Suppose we build a model:

$$
\text{Price}
=
\beta_0+
\beta_1(\text{Size})+
\beta_2(\text{Bedrooms})+
\beta_3(\text{Age})
$$

and obtain:

$$
R^2=0.75
$$

We can say:

> The model explains approximately 75% of the variation in house prices in the dataset, relative to a mean-only baseline.

We **should not automatically say**:

> "The model predicts house prices with 75% accuracy."

That's incorrect.

\(R^2\) is **not accuracy**.

---

# 22. A Visual Way to Think About R-squared

Imagine the variation in the target as a large circle:

```text
Total variation in Y
┌─────────────────────────────┐
│                             │
│     Explained by model      │
│       ┌──────────────┐      │
│       │              │      │
│       │     80%      │      │
│       │              │      │
│       └──────────────┘      │
│                             │
│      Unexplained 20%        │
│                             │
└─────────────────────────────┘
```

Then:

$$
R^2=0.80
$$

means approximately 80% of the variation is accounted for by the regression model relative to the mean baseline.

---

# 23. The Complete Regression Picture

```text
                    Regression Model
                           │
                           ▼
                  Predicted values ŷ
                           │
             ┌─────────────┴─────────────┐
             │                           │
             ▼                           ▼
       Compare with y               Compare with mean
             │                           │
             ▼                           ▼
        Residual error              Total variation
             │                           │
             └─────────────┬─────────────┘
                           ▼
                         R²
                           │
                           ▼
              Fraction of variation
                 explained by model
```

---

# 24. Important Distinction: Explanation vs Prediction

R-squared is often described as "variance explained," but don't interpret that as proving a scientific explanation.

It is a **descriptive/model-fit measure**.

For example:

$$
R^2=0.85
$$

means the fitted model accounts for a large fraction of observed variation in \(Y\).

It doesn't establish that the predictors **caused** that variation.

---

# 25. Common Mistakes

### ❌ "R² = 0.8 means the model is 80% accurate."

Wrong.

### ❌ "R² = 0.8 means the prediction error is 20%."

Wrong.

### ❌ "R² = 0.8 proves the predictors cause Y."

Wrong.

### ❌ "Higher R² always means a better model."

Not necessarily—especially for training data.

### ❌ "R² can never be negative."

Wrong. It can be negative for some models/evaluation settings, particularly out-of-sample.

### ❌ "R² tells us the direction of the relationship."

No.

For direction, look at coefficients or correlation where appropriate.

### ❌ "R² = 0 means there is no relationship of any kind."

Not necessarily. \(R^2\) concerns the model and its ability to explain variation; nonlinear relationships may exist that a linear model doesn't capture.

---

# 26. R-squared vs Adjusted R-squared

|                                                                  | R²                   | Adjusted R²           |
| ---------------------------------------------------------------- | -------------------- | --------------------- |
| Measures model fit                                               | ✅                    | ✅                     |
| Rewards adding predictors                                        | Yes                  | Only if useful enough |
| Can decrease when predictor added?                               | No, for training OLS | Yes                   |
| Penalizes complexity                                             | ❌                    | ✅                     |
| Useful for comparing models with different numbers of predictors | Limited              | More useful           |

---

# 27. Interview-Ready Answer

> **R-squared, or the coefficient of determination, measures the proportion of variation in the dependent variable that is explained by a regression model relative to a mean-only baseline. It is calculated as \(R^2=1-\frac{SS_{res}}{SS_{tot}}\). For example, an \(R^2\) of 0.80 means the model explains about 80% of the variation in the observed response values. However, R-squared is not prediction accuracy and does not imply causation. We should also evaluate test-set performance, residuals, and metrics such as RMSE or MAE.**

---

# 🧠 Mental Model

Think:

> **R² = "How much of the variation in Y does my model explain compared with just predicting the average?"**

```text
Predict the mean
       ↓
Baseline
       ↓
How much variation remains?
       ↓
Regression model
       ↓
How much did we explain?
       ↓
       R²
```

### One-line takeaway

$$
\boxed{
R^2=
1-\frac{\text{Unexplained Variation}}
{\text{Total Variation}}
}
$$

**Higher \(R^2\)** generally means the model explains more variation in the data, but **higher \(R^2\) does not automatically mean better predictions, causation, or a better model.**
