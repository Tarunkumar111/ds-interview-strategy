# The Essence of Linear Regression!!!

## 1. What is Linear Regression?

**Linear regression** is a statistical method used to understand and predict the relationship between a **dependent variable \(Y\)** and one or more **independent variables \(X\)**.

The simplest case is **simple linear regression**:

$$
\boxed{\hat y=b_0+b_1x}
$$

where:

* \(\hat y\) = predicted value of \(Y\)
* \(b_0\) = intercept
* \(b_1\) = slope
* \(x\) = predictor/input

The essence is:

> **Find the straight line that best describes the relationship between \(X\) and \(Y\).**

![linear regression](images/linear_regression.png)

---

# 2. The Simplest Example

Suppose we want to predict someone's salary from years of experience.

| Experience | Salary |
| ---------: | -----: |
|          1 |   ₹30k |
|          2 |   ₹35k |
|          3 |   ₹42k |
|          4 |   ₹48k |
|          5 |   ₹55k |

We might fit:

$$
\hat y=25+6x
$$

Here:

* \(25\) = intercept
* \(6\) = slope

For someone with 4 years of experience:

$$
\hat y=25+6(4)
$$

$$
=49
$$

So the predicted salary is:

$$
\boxed{₹49k}
$$

---

# 3. What Does the Line Actually Mean?

The line:

$$
\hat y=b_0+b_1x
$$

has two important pieces.

### Intercept \(b_0\)

The predicted value of \(Y\) when:

$$
X=0
$$

### Slope \(b_1\)

The expected change in predicted \(Y\) for a **one-unit increase in \(X\)**.

If:

$$
b_1=6
$$

then:

> Each additional year of experience is associated with an increase of ₹6k in predicted salary.

### Important

"Associated with" is safer than "causes."

Regression by itself does **not establish causation**.

---

# 4. The Real Data Don't Usually Fall Perfectly on a Line

Real-world data look more like:

```text
Salary
  |
60|                 •
50|             •  •
40|        •  •
30|    •
  |
  +------------------------ Experience
      1   2   3   4   5
```

The regression line tries to pass through the data in a way that captures the overall pattern.

Some points will be above the line.

Some will be below it.

That's normal.

---

# 5. Predictions vs Actual Values

For each observation:

$$
\text{Residual}=y-\hat y
$$

where:

* \(y\) = actual value
* \(\hat y\) = predicted value

Example:

Actual salary:

$$
y=52
$$

Predicted salary:

$$
\hat y=49
$$

Residual:

$$
52-49=3
$$

So the model underpredicted by ₹3k.

---

# 6. The Most Important Idea: Residuals

Think of the regression line as making predictions.

The **residual** is the vertical distance between the actual point and the line.

```text
Y
│
│          • Actual
│          │
│          │  Residual
│          │
│      ────×──────── Regression line
│          ↑
│       Prediction
│
└──────────────── X
```

A good-fitting model generally has relatively small residuals, though "good" also depends on the problem and assumptions.

---

# 7. Why "Least Squares"?

Linear regression commonly finds the line by minimizing the **sum of squared residuals**.

$$
\boxed{
SS_{\text{res}}=\sum_{i=1}^{n}(y_i-\hat y_i)^2
}
$$

The chosen line is the one that minimizes this quantity among linear models.

That's why it's called:

> **Ordinary Least Squares (OLS) regression.**

---

# 8. Why Square the Residuals?

Suppose residuals are:

$$
-5,-2,+2,+5
$$

If we simply add them:

$$
-5-2+2+5=0
$$

It would look like there is no error.

But there clearly is error.

Squaring gives:

$$
25+4+4+25=58
$$

Now large errors are properly reflected.

### Another benefit

Squaring also penalizes large errors more heavily.

For example:

$$
2^2=4
$$

but:

$$
10^2=100
$$

So a large prediction error has a much larger impact on the objective.

---

# 9. What Is the Regression Actually Trying to Do?

At its heart:

```text
Data
 ↓
Try possible lines
 ↓
Calculate residuals
 ↓
Square residuals
 ↓
Add them
 ↓
Choose line with smallest total
 ↓
Best-fitting least-squares line
```

That's the essence of ordinary linear regression.

---

# 10. What Does "Best-Fitting Line" Mean?

It does **not** mean:

> The line passes through the most points.

It means:

> The line minimizes the sum of squared residuals.

For example, we could have:

```text
Line A → large residuals
Line B → smaller residuals
Line C → smallest sum of squared residuals
```

OLS chooses:

$$
\boxed{\text{Line C}}
$$

---

# 11. Intercept and Slope

Consider:

$$
\hat y=10+5x
$$

### Intercept

$$
b_0=10
$$

When \(x=0\):

$$
\hat y=10
$$

### Slope

$$
b_1=5
$$

For every one-unit increase in \(x\):

$$
\hat y\text{ increases by }5
$$

So:

```text
X increases by 1
       ↓
Predicted Y increases by 5
```

---

# 12. Positive vs Negative Slope

### Positive slope

$$
b_1>0
$$

As \(X\) increases, predicted \(Y\) increases.

```text
Y
│          /
│        /
│      /
│    /
│  /
└────────── X
```

### Negative slope

$$
b_1<0
$$

As \(X\) increases, predicted \(Y\) decreases.

```text
Y
│\
│ \
│  \
│   \
│    \
└────────── X
```

### Zero slope

$$
b_1=0
$$

The model predicts the same value regardless of \(X\).

---

# 13. Simple vs Multiple Linear Regression

### Simple linear regression

One predictor:

$$
\boxed{\hat y=b_0+b_1x}
$$

Example:

$$
\text{Salary}=b_0+b_1(\text{Experience})
$$

### Multiple linear regression

Multiple predictors:

$$
\boxed{
\hat y=b_0+b_1x_1+b_2x_2+\cdots+b_px_p
}
$$

Example:

$$
\text{Salary}
=
b_0+
b_1(\text{Experience})+
b_2(\text{Education})+
b_3(\text{Job Level})
$$

Now each coefficient describes the expected change in \(Y\) associated with a one-unit change in that predictor, **holding the other included predictors constant**, under the model.

---

# 14. A Very Important Interpretation of Multiple Regression

Suppose:

$$
\text{Salary}
=
20+5(\text{Experience})+3(\text{Education})
$$

The coefficient:

$$
b_1=5
$$

means:

> Holding education constant, one additional unit of experience is associated with an increase of 5 units in predicted salary.

That "holding other variables constant" interpretation is extremely important.

---

# 15. Linear Regression Does NOT Mean the Data Must Look Perfectly Linear

"Linear" refers to the model being **linear in its coefficients/parameters**.

For example:

$$
y=b_0+b_1x+b_2x^2
$$

is still a linear regression model in the coefficients \(b_0,b_1,b_2\), even though the relationship with \(x\) is curved.

But:

$$
y=e^{b_0+b_1x}
$$

is nonlinear in the parameters as written.

So don't interpret "linear regression" as simply:

> "The graph must be a straight line."

---

# 16. Linear Regression and Correlation

You recently learned about Pearson correlation.

For simple linear regression with one predictor and an intercept:

$$
\boxed{R^2=r^2}
$$

So if:

$$
r=0.8
$$

then:

$$
R^2=0.64
$$

But they answer somewhat different questions.

### Correlation

> How strongly and in what direction are \(X\) and \(Y\) linearly associated?

### Regression

> What relationship can we use to estimate/predict \(Y\) from \(X\)?

---

# 17. Linear Regression and R-squared

R-squared measures how much variation in \(Y\) is explained by the model relative to a mean-only baseline.

$$
\boxed{
R^2=1-\frac{SS_{\text{res}}}{SS_{\text{tot}}}
}
$$

For example:

$$
R^2=0.75
$$

means the model explains approximately 75% of the variation in \(Y\) relative to that baseline, on the data where \(R^2\) is being evaluated.

### Important

It does **not** mean:

> "The model is 75% accurate."

---

# 18. Linear Regression and Residuals

After fitting a regression model, we should examine the residuals.

Ideally, residuals should not show obvious patterns.

For example:

```text
Good:

Residual
  |
 +|   •    •
  |      •
  | •       •
  |    •
 -|       •
  +---------------- X
```

But this pattern is concerning:

```text
Residual
  |
 +| •           •
  |   •       •
  |     •   •
  |       •
 -|
  +---------------- X
```

A curved pattern suggests the linear model may be missing systematic structure.

---

# 19. Common Assumptions

Classical linear regression inference commonly relies on assumptions such as:

### 1. Linearity

The conditional mean relationship is appropriately represented by the model.

### 2. Independence

Observations/errors are appropriately independent for the analysis.

### 3. Constant variance

Residual variability is approximately constant across relevant predictor values (**homoscedasticity**).

### 4. Appropriate error distribution

Normality of errors is particularly relevant for some small-sample inference, such as exact t/F procedures; it is not required simply to fit OLS.

### 5. No problematic multicollinearity

In multiple regression, predictors shouldn't be so strongly related that coefficient estimates become unstable or difficult to interpret.

These assumptions depend on what you're trying to do—prediction, estimation, hypothesis testing, etc.

---

# 20. What Happens If Assumptions Are Violated?

For example, suppose residual variance increases as \(X\) increases:

```text
Residual
  |
  | •
  | • •
  |  •  •
  |    •   •
  |      •     •
  +---------------- X
```

This is **heteroscedasticity**.

OLS coefficients can still sometimes be useful, but standard errors and inference may be wrong if the issue isn't handled appropriately.

Possible approaches include:

* transformations
* robust standard errors
* weighted least squares
* different models

The appropriate solution depends on the problem.

---

# 21. Linear Regression Is Not Automatically Causal

Suppose:

$$
\text{Ice Cream Sales}
$$

and:

$$
\text{Swimming Accidents}
$$

have a strong relationship.

Regression might show a strong association.

But that doesn't mean ice cream causes accidents.

A third variable—temperature—could influence both.

```text
           Temperature
           ↙         ↘
Ice Cream Sales     Swimming Accidents
```

Therefore:

$$
\boxed{\text{Regression association}\neq\text{causation}}
$$

Causal conclusions require an appropriate causal design and assumptions.

---

# 22. Prediction vs Explanation

Linear regression can be used for both.

### Prediction

> Given \(X\), what value of \(Y\) should I predict?

Example:

> Predict house price from size and location.

### Explanation/estimation

> How is \(Y\) associated with \(X\), after accounting for other variables?

Example:

> Estimate the association between experience and salary while holding other included predictors constant.

These are related but not identical goals.

---

# 23. Confidence Intervals for Regression Coefficients

Suppose our estimated coefficient is:

$$
b_1=5
$$

and its 95% confidence interval is:

$$
(3,7)
$$

We can report:

> The estimated slope is 5, with a 95% CI of 3 to 7.

This communicates uncertainty around the estimated coefficient.

This connects directly to what you just learned about **confidence intervals**.

---

# 24. Hypothesis Testing in Regression

We can test:

$$
H_0:\beta_1=0
$$

against:

$$
H_1:\beta_1\ne0
$$

A common test statistic is:

$$
t=\frac{b_1-0}{SE(b_1)}
$$

A small p-value provides evidence against the null hypothesis that the coefficient is zero under the specified model.

But remember:

> Statistical significance does not automatically mean the effect is practically important or causal.

---

# 25. Linear Regression: The Big Picture

You can connect almost everything you've learned:

```text
                 Linear Regression
                        │
          ┌─────────────┼─────────────┐
          ↓             ↓             ↓
      Coefficients    Residuals      Predictions
          │             │             │
          ↓             ↓             ↓
       Slope         Error         ŷ = b₀+b₁x
          │
          ↓
   Standard Error
          │
          ↓
 Confidence Interval
          │
          ↓
   Hypothesis Test
          │
          ↓
       p-value

          +
          
      R-squared
          ↓
   Explained variation
```

---

# 26. The Essence in One Example

Suppose we want to predict salary from experience.

### Step 1 — Collect data

$$
(X,Y)
$$

Experience + salary.

### Step 2 — Fit a line

$$
\hat y=b_0+b_1x
$$

### Step 3 — Make predictions

$$
\hat y_i
$$

### Step 4 — Calculate residuals

$$
e_i=y_i-\hat y_i
$$

### Step 5 — Minimize squared residuals

$$
\sum e_i^2
$$

### Step 6 — Evaluate the model

Use things such as:

* \(R^2\)
* RMSE
* MAE
* residual diagnostics
* test-set performance

### Step 7 — Quantify uncertainty

For coefficients, predictions, or other quantities, use appropriate standard errors and confidence/prediction intervals.

---

# 27. The Ultimate Mental Model

Think of linear regression as:

> **Finding a mathematical relationship that summarizes how an outcome changes with one or more predictors, while making the prediction errors as small as possible under the chosen fitting criterion.**

The basic flow is:

```text
Data
  ↓
Choose X and Y
  ↓
Fit regression model
  ↓
ŷ = b₀ + b₁X
  ↓
Make predictions
  ↓
Calculate residuals
  ↓
Minimize squared residuals
  ↓
Evaluate fit + assumptions
  ↓
Interpret coefficients + uncertainty
```

---

# Interview-Ready Answer

> **Linear regression is a statistical method for modeling the relationship between a dependent variable and one or more predictors. In simple linear regression, we model the predicted outcome as \(\hat y=b_0+b_1x\). Ordinary least squares estimates the coefficients by minimizing the sum of squared residuals between observed and predicted values. The slope describes the expected change in the predicted outcome for a one-unit increase in the predictor, while \(R^2\) describes the proportion of variation explained relative to a mean-only baseline. Linear regression can be used for prediction and estimation, but regression alone does not establish causation.**

## 🧠 One-line takeaway

$$
\boxed{\text{Linear Regression}=\text{Fit the best relationship between }X\text{ and }Y\text{ to make predictions and understand associations.}}
$$

**The deepest idea:**
**Data → fit a line/model → minimize prediction errors → interpret coefficients → quantify uncertainty → check whether the model is appropriate.**
