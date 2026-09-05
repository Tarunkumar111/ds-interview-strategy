# Multiple Regression, Clearly Explained!!!

Multiple regression is an extension of **simple linear regression** where we use **multiple independent variables (predictors/features)** to predict or explain one dependent variable.

---

## 1. Simple Linear Regression vs Multiple Regression

### Simple Linear Regression

Uses **one predictor**:

$$
\hat{y}=b_0+b_1x
$$

Example:

> Predict salary using years of experience.

```text
Experience ───────► Salary
```

---

### Multiple Linear Regression

Uses **multiple predictors**:

$$
\hat{y}=b_0+b_1x_1+b_2x_2+\cdots+b_px_p
$$

For example, salary might depend on:

* Experience
* Education
* Age
* Job level

```text
Experience ───────┐
Education ────────┤
Age ──────────────┼────► Salary
Job Level ────────┘
```

The main idea is:

> **Use several variables together to predict or explain one outcome.**

---

# 2. A Real-World Example

Suppose we want to predict someone's salary.

We have:

| Experience | Education | Age | Salary |
| ---------: | --------: | --: | -----: |
|          2 |        12 |  24 |     35 |
|          4 |        16 |  28 |     50 |
|          6 |        16 |  32 |     65 |
|          8 |        18 |  36 |     80 |
|         10 |        18 |  40 |     95 |

We could build:

$$
\hat{Salary}
=
b_0
+b_1(Experience)
+b_2(Education)
+b_3(Age)
$$

The model tries to find the values of:

$$
b_0,b_1,b_2,b_3
$$

that make predictions as close as possible to the observed salaries.

---

# 3. What Do the Coefficients Mean?

Suppose our fitted model is:

$$
\hat{Salary}
=
20
+5(Experience)
+2(Education)
+1(Age)
$$

Here:

* \(20\) = intercept
* \(5\) = experience coefficient
* \(2\) = education coefficient
* \(1\) = age coefficient

The important part is how we interpret the coefficients.

### Experience coefficient = 5

We say:

> Holding education and age constant, a one-unit increase in experience is associated with a 5-unit increase in predicted salary.

### Education coefficient = 2

> Holding experience and age constant, a one-unit increase in education is associated with a 2-unit increase in predicted salary.

### Age coefficient = 1

> Holding experience and education constant, a one-unit increase in age is associated with a 1-unit increase in predicted salary.

---

# 4. "Holding Other Variables Constant" Is Important

This is one of the most important ideas in multiple regression.

Suppose:

$$
Salary=20+5Experience+2Education+Age
$$

When interpreting the experience coefficient:

> We compare people with different experience **while keeping the other included predictors constant**.

Why?

Because experience, education, and age may all be related to salary.

Multiple regression attempts to estimate the **partial association** of each predictor after accounting for the other predictors in the model.

### Mental model

```text
Experience ───────►
                   │
Education ────────►├──► Salary
                   │
Age ──────────────►
```

Each coefficient represents the contribution associated with that predictor **conditional on the other predictors in the model**.

---

# 5. How Does Multiple Regression Find the Best Model?

Just like simple linear regression, multiple regression commonly uses **Ordinary Least Squares (OLS)**.

The model produces predictions:

$$
\hat y_1,\hat y_2,\ldots,\hat y_n
$$

Then we calculate residuals:

$$
e_i=y_i-\hat y_i
$$

OLS chooses the coefficients that minimize:

$$
\sum_{i=1}^{n}(y_i-\hat y_i)^2
$$

In simple regression, we are fitting a **line**.

In multiple regression, with two predictors, we can visualize the fitted relationship as a **plane**.

With more predictors, it becomes a higher-dimensional hyperplane that we can't easily visualize.

![Multiple Regression](images/Multiple Regression.png)

---

# 6. Why Do We Square the Errors?

Suppose the actual and predicted values are:

| Actual | Predicted | Residual |
| -----: | --------: | -------: |
|     50 |        48 |        2 |
|     60 |        63 |       -3 |
|     70 |        69 |        1 |

If we simply add residuals:

$$
2+(-3)+1=0
$$

Positive and negative errors cancel.

So we square them:

$$
2^2+(-3)^2+1^2
$$

$$
=4+9+1=14
$$

The model tries to make this total as small as possible.

---

# 7. Multiple Regression in Matrix Form

When there are many predictors, we often write the model as:

$$
\mathbf y=\mathbf X\boldsymbol\beta+\boldsymbol\epsilon
$$

Where:

* \(\mathbf y\) = outcome values
* \(\mathbf X\) = predictor/features matrix
* \(\boldsymbol\beta\) = regression coefficients
* \(\boldsymbol\epsilon\) = errors

For example:

$$
\begin{bmatrix}
y_1\\
y_2\\
y_3
\end{bmatrix}
=
\begin{bmatrix}
1&x_{11}&x_{12}\\
1&x_{21}&x_{22}\\
1&x_{31}&x_{32}
\end{bmatrix}
\begin{bmatrix}
b_0\\
b_1\\
b_2
\end{bmatrix}
+
\begin{bmatrix}
\epsilon_1\\
\epsilon_2\\
\epsilon_3
\end{bmatrix}
$$

The column of 1s represents the intercept.

---

# 8. Simple vs Multiple Regression

| Feature                    | Simple Regression              | Multiple Regression                                                       |
| -------------------------- | ------------------------------ | ------------------------------------------------------------------------- |
| Predictors                 | 1                              | 2 or more                                                                 |
| Example                    | Salary ~ Experience            | Salary ~ Experience + Education + Age                                     |
| Equation                   | \(b_0+b_1x\)                   | \(b_0+b_1x_1+\cdots+b_px_p\)                                              |
| Visualization              | Line                           | Plane / hyperplane                                                        |
| Coefficient interpretation | Effect/association of X with Y | Effect/association of X with Y holding other included predictors constant |

---

# 9. Why Use Multiple Regression?

Imagine:

> Does advertising spending increase sales?

Suppose companies that spend more on advertising also tend to have:

* larger populations of customers
* bigger sales teams
* larger budgets

If we only use advertising:

$$
Sales \sim Advertising
$$

we might attribute some effects of other variables to advertising.

We can instead include relevant variables:

$$
Sales
=
b_0+
b_1Advertising+
b_2SalesTeam+
b_3CustomerBase
$$

This allows us to **account for those measured variables** when estimating the association between advertising and sales.

---

# 10. Multiple Regression Does NOT Automatically Prove Causation

This is extremely important.

Suppose:

$$
Sales=b_0+b_1Advertising+b_2CustomerBase
$$

and we find:

$$
b_1>0
$$

We cannot automatically conclude:

> "Advertising causes sales to increase."

There could still be:

* omitted variables
* confounding
* selection bias
* measurement error
* reverse causality
* other sources of bias

Regression can identify associations and estimate conditional relationships. **Causal conclusions require appropriate causal design/assumptions.**

---

# 11. Multicollinearity

One of the major issues in multiple regression is **multicollinearity**.

It occurs when predictors are strongly related to each other.

For example:

```text
Age ─────────────►
                  │
                  ├── strongly related
                  │
Years of Experience
```

Suppose:

* Age and experience are highly correlated.
* Both are included in the model.

The model may have difficulty determining how much of the relationship with salary should be attributed to each variable.

### Consequences

Multicollinearity can cause:

* unstable coefficients
* large standard errors
* coefficients that change substantially when variables are added/removed
* difficulty interpreting individual coefficients

### Important

Multicollinearity doesn't necessarily make predictions terrible.

It is particularly problematic when your goal is to interpret **individual coefficients**.

---

# 12. Dummy Variables for Categorical Data

Regression can also use categorical predictors.

Suppose we have:

```text
Education:
Bachelor
Master
PhD
```

We can't directly put these words into the equation.

Instead, we can encode categories using indicator/dummy variables.

For example:

$$
Salary=
b_0+
b_1Experience+
b_2Master+
b_3PhD
$$

Bachelor's degree becomes the **reference category**.

Then:

* \(b_2\) compares Master vs Bachelor
* \(b_3\) compares PhD vs Bachelor

while holding the other included predictors constant.

---

# 13. Interaction Effects

Sometimes the effect of one predictor depends on another predictor.

For example:

> Does experience affect salary differently depending on education?

We can include an interaction:

$$
Salary=
b_0+b_1Experience+b_2Education
+b_3(Experience\times Education)
$$

The interaction term allows the relationship between experience and salary to change depending on education.

### Without interaction

```text
Experience → Salary
```

Same slope for everyone.

### With interaction

```text
             ┌── Bachelor
Experience ──┼── Master
             └── PhD

Different relationships can be modeled.
```

This is a powerful extension of multiple regression.

---

# 14. \(R^2\) in Multiple Regression

\(R^2\) measures how much variation in the outcome is explained by the predictors relative to a mean-only model.

A common formula is:

$$
R^2=1-\frac{SS_{Residual}}{SS_{Total}}
$$

For example:

$$
R^2=0.80
$$

means the model explains **80% of the sample variation in the outcome relative to the mean-only baseline**, under the usual definition.

It does **not** mean:

> "The model is 80% accurate."

And it does not mean:

> "The predictors cause 80% of the outcome."

---

# 15. Why Adjusted \(R^2\)?

Adding predictors to an OLS model cannot decrease training \(R^2\), even if a new predictor is not useful.

That's why we have **adjusted \(R^2\)**.

$$
Adjusted\ R^2
=
1-(1-R^2)\frac{n-1}{n-p-1}
$$

where:

* \(n\) = number of observations
* \(p\) = number of predictors

Adjusted \(R^2\) penalizes the model for adding predictors.

### Mental model

```text
R²
↓
Rewards explained variation

Adjusted R²
↓
Rewards explained variation
+
penalizes unnecessary complexity
```

---

# 16. Testing Individual Coefficients

For a coefficient \(b_j\), we can test:

$$
H_0:\beta_j=0
$$

against, for example:

$$
H_1:\beta_j\ne0
$$

A common test statistic is:

$$
t=\frac{b_j}{SE(b_j)}
$$

A small p-value provides evidence against \(H_0\), under the model assumptions.

### Example

Suppose:

$$
b_1=5
$$

and:

$$
SE(b_1)=1
$$

Then:

$$
t=\frac{5}{1}=5
$$

A corresponding p-value can be calculated using the appropriate t distribution.

---

# 17. Confidence Intervals for Coefficients

We can also construct a confidence interval:

$$
b_j\pm t^*SE(b_j)
$$

For example:

$$
b_1=5
$$

with a 95% CI:

$$
[3,7]
$$

A common interpretation is:

> Under the model and repeated-sampling framework, the procedure used to construct the interval captures the true coefficient in about 95% of repeated samples.

For practical interpretation, we might say the data are consistent with a coefficient between 3 and 7 under the model assumptions.

---

# 18. Assumptions of Multiple Linear Regression

For reliable inference, we usually care about several assumptions.

### 1. Linearity

The expected outcome should be appropriately modeled as a linear function of the predictors.

### 2. Independence

Observations/errors should have an appropriate independence structure for the analysis.

### 3. Constant variance

The error variance should be reasonably constant across relevant fitted values/predictor patterns when using the standard homoscedastic model.

### 4. Appropriate error distribution

For small-sample inference, approximately normal errors are often useful.

### 5. No severe multicollinearity

Predictors shouldn't have problematic levels of linear dependence.

### 6. No extreme influential observations

A small number of observations shouldn't disproportionately determine the fitted model.

---

# 19. Residual Diagnostics

After fitting the model, don't just look at \(R^2\).

Look at the residuals.

Useful plots include:

```text
Residuals vs Fitted
        ↓
Check nonlinearity / changing variance

Q-Q Plot
        ↓
Check approximate normality of residuals

Residuals vs Leverage
        ↓
Identify influential observations
```

For example, a curved residual pattern may indicate that the linear specification is missing nonlinear structure.

---

# 20. Prediction vs Explanation

Multiple regression can have two different goals.

### Prediction

> Can I accurately predict \(Y\)?

Example:

> Predict house prices using size, location, bedrooms, and age.

### Explanation / inference

> How is \(Y\) associated with a particular predictor after accounting for other included predictors?

Example:

> How is house price associated with floor area after accounting for location and age?

These are related but **not identical goals**.

A model that predicts well isn't automatically a model that gives causal or scientifically meaningful coefficient interpretations.

---

# 21. Multiple Regression in Python

Using `scikit-learn`:

```python
from sklearn.linear_model import LinearRegression

X = df[["experience", "education", "age"]]
y = df["salary"]

model = LinearRegression()

model.fit(X, y)
```

Get the intercept:

```python
model.intercept_
```

Get the coefficients:

```python
model.coef_
```

Predict:

```python
predictions = model.predict(X)
```

Evaluate:

```python
from sklearn.metrics import r2_score, mean_absolute_error
import numpy as np
from sklearn.metrics import mean_squared_error

r2 = r2_score(y, predictions)

mae = mean_absolute_error(y, predictions)

rmse = np.sqrt(mean_squared_error(y, predictions))
```

---

# 22. A Complete Workflow

A practical multiple regression workflow looks like this:

```text
Raw Data
   ↓
Understand the variables
   ↓
Clean the data
   ↓
Explore relationships
   ↓
Choose predictors
   ↓
Encode categorical variables
   ↓
Train/Test Split
   ↓
Fit Multiple Regression
   ↓
Make Predictions
   ↓
Evaluate Performance
   ↓
Check Residuals & Assumptions
   ↓
Check Multicollinearity / Influence
   ↓
Improve Model
```

---

# 23. Multiple Regression vs Correlation

Correlation measures the **pairwise linear association** between two variables.

Multiple regression can examine the relationship between an outcome and **several predictors simultaneously**.

For example:

### Correlation

$$
r(Experience,Salary)
$$

asks:

> How strongly are experience and salary linearly associated?

### Multiple regression

$$
Salary=
b_0+b_1Experience+b_2Education+b_3Age
$$

asks:

> How is salary associated with experience after accounting for education and age included in the model?

---

# 24. Multiple Regression vs Simple Regression

Think of it like this:

```text
Simple Regression

X ─────────► Y


Multiple Regression

X₁ ────────┐
X₂ ────────┤
X₃ ────────┼────► Y
X₄ ────────┘
```

Simple regression:

> One predictor.

Multiple regression:

> Multiple predictors.

---

# 25. Common Mistakes

### ❌ "Multiple regression means multiple outcomes."

No.

Multiple regression usually means:

> **One outcome + multiple predictors.**

---

### ❌ "A significant coefficient proves causation."

No.

Regression alone does not establish causality.

---

### ❌ "A high \(R^2\) means the model is good."

Not necessarily.

You should also consider:

* test-set performance
* residuals
* model assumptions
* overfitting
* data quality
* prediction goal

---

### ❌ "Adding more variables always improves the model."

Training \(R^2\) won't decrease, but extra variables can:

* add noise
* increase complexity
* create multicollinearity
* hurt test performance
* make interpretation harder

---

### ❌ "The coefficient is the effect regardless of other variables."

Not necessarily.

In multiple regression, coefficient interpretation is conditional on the other included predictors and the model specification.

---

# 26. The Big Picture

Connect everything you've learned:

```text
                 Multiple Regression
                        │
          ┌─────────────┴─────────────┐
          ↓                           ↓
     Predict Y                  Understand
          │                     associations
          ↓                           │
   Several predictors          Coefficients
          │                           │
          └─────────────┬─────────────┘
                        ↓
                 Fit using OLS
                        ↓
                Minimize squared
                    residuals
                        ↓
              Evaluate the model
                        ↓
       ┌────────────────┼────────────────┐
       ↓                ↓                ↓
      R²             Residuals       Test-set error
       │                │                │
       └────────────────┼────────────────┘
                        ↓
             Check assumptions,
        multicollinearity & influence
```

---

# 🧠 Mental Model

Think of multiple regression as:

> **"I have one outcome and several variables that might help explain or predict it. I'll find the combination of coefficients that best fits the data, while accounting for the other predictors included in the model."**

---

# 🎯 Interview-Ready Answer

> **Multiple linear regression is a statistical method used to model or predict one dependent variable using two or more independent variables. The model is typically written as \(\hat y=b_0+b_1x_1+\cdots+b_px_p\), and ordinary least squares estimates the coefficients by minimizing the sum of squared residuals. Each coefficient represents the change in predicted \(Y\) associated with a one-unit change in that predictor, holding the other included predictors constant.**

---

## One-Line Takeaway

> **Multiple regression uses multiple predictors to model one outcome, with each coefficient describing the predictor's conditional linear association with the outcome given the other variables in the model.**
