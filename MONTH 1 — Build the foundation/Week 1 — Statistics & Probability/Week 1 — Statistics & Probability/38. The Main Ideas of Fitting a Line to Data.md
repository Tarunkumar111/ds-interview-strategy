# The Main Ideas of Fitting a Line to Data

### The Main Ideas of Least Squares and Linear Regression

The central idea is surprisingly simple:

> **We have a bunch of data points, and we want to find the straight line that best summarizes the relationship between \(X\) and \(Y\).**

That line can then be used to **understand the relationship** and **make predictions**.

![fitting straight line](images/fitting_straight_line.png)

---

# 1. Start With the Data

Suppose we want to understand whether **years of experience** are related to **salary**.

We collect observations:

| Experience \(X\) | Salary \(Y\) |
| ---------------: | -----------: |
|                1 |           32 |
|                2 |           35 |
|                3 |           41 |
|                4 |           47 |
|                5 |           53 |

If we plot them, we might see something like:

```text
Salary
  |
55|                 •
50|             •
45|
40|        •
35|    •
30| •
  +---------------------- Experience
    1   2   3   4   5
```

There appears to be an upward trend.

We could try to summarize that trend with a straight line.

---

# 2. The Line

A straight line can be written as:

$$
\boxed{\hat y=b_0+b_1x}
$$

where:

* \(\hat y\) = predicted value
* \(b_0\) = intercept
* \(b_1\) = slope
* \(x\) = predictor

For example:

$$
\hat y=25+5x
$$

This means:

* when \(x=0\), predicted \(y=25\)
* every 1-unit increase in \(x\) increases predicted \(y\) by 5

---

# 3. But Which Line?

There are infinitely many possible lines.

For example:

```text
Line A  ─────────────
Line B       ╱
Line C     ╱
Line D   ╱
```

Some lines will fit the data better than others.

So we need a way to define:

> **What does "best-fitting line" mean?**

That's where **least squares** comes in.

---

# 4. Predictions and Residuals

For every data point, the line makes a prediction:

$$
\hat y_i
$$

But the actual observation is:

$$
y_i
$$

The difference is called the **residual**:

$$
\boxed{e_i=y_i-\hat y_i}
$$

For example:

Actual salary:

$$
y=50
$$

Predicted salary:

$$
\hat y=47
$$

Residual:

$$
e=50-47=3
$$

The model underpredicted by 3.

---

# 5. Visualizing a Residual

The residual is the **vertical distance** between the actual point and the regression line.

```text
Y
│
│              • Actual
│              │
│              │  Residual
│              │
│         ─────×────────
│              ↑
│          Prediction
│
└──────────────────── X
```

Every point has its own residual.

Some residuals are positive.

Some are negative.

---

# 6. Why Can't We Just Add the Residuals?

Because positive and negative residuals can cancel.

Suppose:

$$
e=[-5,-2,+2,+5]
$$

Then:

$$
-5-2+2+5=0
$$

That would make it look like there is no error.

But there clearly is error.

So we **square the residuals**.

$$
(-5)^2+(-2)^2+(2)^2+(5)^2
$$

$$
=25+4+4+25
$$

$$
=58
$$

Now all errors contribute positively.

---

# 7. Least Squares

The **least-squares line** is the line that minimizes:

$$
\boxed{
\sum_{i=1}^{n}(y_i-\hat y_i)^2
}
$$

In words:

> **Choose the line that produces the smallest possible sum of squared residuals.**

That's the fundamental idea behind **ordinary least squares (OLS)**.

---

# 8. The Whole Process

Think of it like this:

```text
Data points
    ↓
Try a line
    ↓
Calculate predictions
    ↓
Calculate residuals
    ↓
Square residuals
    ↓
Add squared residuals
    ↓
Try to make the total as small as possible
    ↓
Best-fitting line
```

This is the heart of least squares.

---

# 9. Why Is Squaring Useful?

Squaring residuals does two important things.

### 1. Prevents cancellation

$$
(-5)^2=25
$$

$$
(+5)^2=25
$$

Both count as errors.

### 2. Penalizes large errors more heavily

Compare:

$$
2^2=4
$$

with:

$$
10^2=100
$$

An error of 10 contributes **25 times** as much to squared error as an error of 2.

So least squares strongly discourages large residuals.

---

# 10. What Does the Slope Tell Us?

Suppose:

$$
\hat y=20+6x
$$

The slope is:

$$
b_1=6
$$

This means:

> For a one-unit increase in \(X\), the model's predicted \(Y\) increases by 6 units.

For example, if \(X\) is years of experience:

> Each additional year of experience is associated with a 6-unit increase in predicted salary, according to the model.

### Important

This does **not automatically mean experience causes salary to increase by 6**.

Regression association is not automatically causation.

---

# 11. What Does the Intercept Tell Us?

In:

$$
\hat y=20+6x
$$

the intercept is:

$$
b_0=20
$$

It represents the predicted value of \(Y\) when:

$$
x=0
$$

So:

$$
\hat y=20
$$

when:

$$
x=0
$$

### Important caveat

Sometimes \(x=0\) isn't meaningful or isn't within the observed range.

For example, if we're predicting salary from age:

$$
\text{Salary}=b_0+b_1(\text{Age})
$$

the intercept corresponds mathematically to age 0, but that may have little practical meaning.

---

# 12. What Is Linear Regression?

**Linear regression** is the broader statistical method used to model a response as a linear function of predictors.

Simple linear regression:

$$
\boxed{\hat y=b_0+b_1x}
$$

Multiple linear regression:

$$
\boxed{
\hat y=b_0+b_1x_1+b_2x_2+\cdots+b_px_p
}
$$

For example:

$$
\text{Salary}
=
b_0+
b_1(\text{Experience})+
b_2(\text{Education})+
b_3(\text{Job Level})
$$

The coefficients are estimated using methods such as least squares.

---

# 13. Least Squares vs Linear Regression

These terms are related but aren't exactly the same thing.

### Linear regression

The **modeling framework**.

> We model the relationship between the outcome and predictors using a linear form.

### Least squares

A common **fitting method**.

> Choose the coefficients that minimize the sum of squared residuals.

So:

```text
Linear regression
      ↓
Choose model
ŷ = b₀ + b₁x
      ↓
Least squares
      ↓
Find b₀ and b₁
      ↓
Minimize squared residuals
```

---

# 14. Why Does the Line Go Through the "Middle"?

For ordinary least squares regression **with an intercept**, the fitted line passes through:

$$
\boxed{(\bar{x},\bar{y})}
$$

the point formed by the sample means.

So if:

$$
\bar{x}=5
$$

and:

$$
\bar{y}=40
$$

the least-squares line passes through:

$$
(5,40)
$$

This is an important property of OLS.

---

# 15. The Line Doesn't Have to Pass Through Every Point

Real data usually contain noise.

So:

```text
       •
    •     •
      ╱
  •  ╱    •
    ╱
 • ╱
```

The goal isn't to hit every point.

The goal is to find the line that provides the **best overall fit according to the least-squares criterion**.

---

# 16. What Happens When the Data Have More Noise?

Imagine two datasets.

### Dataset A

```text
Y
│        •
│      •
│    •
│  •
│ •
└──────────── X
```

Very little scatter.

### Dataset B

```text
Y
│     •       •
│ •        •
│       •
│  •          •
│       •
└──────────── X
```

Much more scatter.

Both can have an upward slope, but Dataset A has a much tighter relationship with the line.

This is where concepts such as **residual variation** and **\(R^2\)** become useful.

---

# 17. Connection to R-squared

You just learned about \(R^2\).

Once we fit a line, we can ask:

> **How much of the variation in \(Y\) does this model explain relative to simply predicting the mean?**

That's what \(R^2\) measures.

$$
\boxed{
R^2=1-\frac{SS_{\text{res}}}{SS_{\text{tot}}}
}
$$

So the concepts connect:

```text
Data
 ↓
Fit line
 ↓
Residuals
 ↓
Squared residuals
 ↓
Least squares
 ↓
Regression model
 ↓
R² evaluates explained variation
```

---

# 18. Regression Is About More Than Drawing a Line

Once we've fitted the line, we can use it for:

### Prediction

Given:

$$
x=7
$$

calculate:

$$
\hat y=b_0+b_1(7)
$$

### Understanding associations

Interpret the slope.

### Quantifying uncertainty

Calculate:

* standard errors
* confidence intervals
* prediction intervals
* hypothesis tests

### Evaluating model fit

Use:

* \(R^2\)
* RMSE
* MAE
* residual diagnostics
* test-set performance

---

# 19. A Very Important Distinction: Prediction vs Actual

Suppose:

$$
\hat y=50
$$

That doesn't mean the actual value is exactly 50.

It means:

> According to the fitted model, the predicted value is 50.

The actual observation could be:

$$
y=56
$$

Then:

$$
e=56-50=6
$$

So the model missed by 6.

---

# 20. Why the Line Is Useful

Suppose we have:

$$
\hat y=20+5x
$$

For:

$$
x=1
$$

$$
\hat y=25
$$

For:

$$
x=5
$$

$$
\hat y=45
$$

For:

$$
x=10
$$

$$
\hat y=70
$$

Instead of memorizing every observed data point, the line gives us a **compact mathematical summary** of the overall relationship.

That's one of the biggest advantages of regression.

---

# 21. But Be Careful With Extrapolation

Suppose our data contain experience from:

$$
1\text{ to }10\text{ years}
$$

and we use the model to predict salary at:

$$
30\text{ years}
$$

We're extrapolating far beyond the observed data.

The linear relationship may not continue.

```text
Observed data
|────────────|
1           10

                 ← dangerous extrapolation →
                                      30
```

Regression lines should be interpreted carefully outside the range of the data.

---

# 22. Correlation, Regression, and R²

These three concepts are closely connected:

| Concept               | Main question                                                                   |
| --------------------- | ------------------------------------------------------------------------------- |
| **Correlation \(r\)** | How strong and what direction is the linear association?                        |
| **Regression**        | What relationship can we use to estimate/predict \(Y\) from \(X\)?              |
| **R²**                | How much variation in \(Y\) does the model explain relative to a mean baseline? |

For simple linear regression with an intercept:

$$
\boxed{R^2=r^2}
$$

---

# 23. The Most Important Mathematical Idea

Everything comes back to:

$$
\boxed{
\min_{b_0,b_1}
\sum_{i=1}^{n}
\left(y_i-(b_0+b_1x_i)\right)^2
}
$$

Read this as:

> **Find the intercept and slope that make the total squared prediction error as small as possible.**

That's the mathematical essence of fitting a line using ordinary least squares.

---

# 24. The Big Picture

```text
                  Observed Data
                       │
                       ▼
              Choose linear model
                       │
                       ▼
                 ŷ = b₀ + b₁x
                       │
                       ▼
                 Make predictions
                       │
                       ▼
                Calculate residuals
                       │
                       ▼
              Square the residuals
                       │
                       ▼
              Add squared residuals
                       │
                       ▼
             Minimize the total
                       │
                       ▼
              Least-squares line
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
        Make predictions      Evaluate model
                                 │
                    ┌────────────┼────────────┐
                    ▼            ▼            ▼
                   R²          RMSE       Residuals
```

---

# 🧠 Mental Model

Think of fitting a line as:

> **"I have a cloud of points. I want one straight line that summarizes the overall relationship while keeping the squared prediction errors as small as possible."**

Remember these four things:

### 1. Line

$$
\hat y=b_0+b_1x
$$

### 2. Residual

$$
e=y-\hat y
$$

### 3. Least squares

$$
\min\sum e^2
$$

### 4. Interpretation

> **The slope tells how the predicted outcome changes as the predictor changes.**

---

# Interview-Ready Answer

> **Fitting a line to data means finding a linear relationship that best summarizes the relationship between a predictor \(X\) and an outcome \(Y\). In ordinary least squares regression, we choose the intercept and slope that minimize the sum of squared residuals, where a residual is the difference between an observed value and its predicted value. The resulting line can be used for prediction and to quantify associations, while metrics such as \(R^2\), RMSE, and residual diagnostics help evaluate the model.**

## One-line takeaway

$$
\boxed{
\text{Least Squares}=
\text{Find the line that minimizes the sum of squared residuals.}
}
$$

**That's the core idea behind fitting a line with ordinary linear regression.**
