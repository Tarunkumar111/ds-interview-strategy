# Multiple Regression in Python, Step-by-Step!!!

Multiple regression in Python is used when we want to predict **one target variable using multiple features**.

For example:

> Predict salary using **experience, education, and age**.

We’ll use **Python + pandas + scikit-learn**.

---

# 1. The Multiple Regression Equation

With one predictor:

$$
\hat{y}=b_0+b_1x
$$

With multiple predictors:

$$
\hat{y}
=
b_0+b_1x_1+b_2x_2+\cdots+b_px_p
$$

For our salary example:

$$
\hat{Salary}
=
b_0
+b_1(Experience)
+b_2(Education)
+b_3(Age)
$$

Where:

* \(b_0\) = intercept
* \(b_1\) = experience coefficient
* \(b_2\) = education coefficient
* \(b_3\) = age coefficient

---

# 2. Import the Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import (
    r2_score,
    mean_absolute_error,
    mean_squared_error
)
```

---

# 3. Create the Dataset

Let's create a small example dataset.

```python
data = {
    "experience": [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    "education": [12, 14, 14, 16, 16, 16, 18, 18, 18, 20],
    "age": [22, 24, 25, 27, 29, 31, 33, 35, 37, 40],
    "salary": [30, 35, 40, 48, 52, 58, 65, 72, 78, 88]
}

df = pd.DataFrame(data)

df
```

Our data looks like:

| Experience | Education | Age | Salary |
| ---------: | --------: | --: | -----: |
|          1 |        12 |  22 |     30 |
|          2 |        14 |  24 |     35 |
|          3 |        14 |  25 |     40 |
|        ... |       ... | ... |    ... |
|         10 |        20 |  40 |     88 |

---

# 4. Understand the Data

Before building a model, inspect the dataset.

```python
df.head()
```

Check the shape:

```python
df.shape
```

Check data types:

```python
df.info()
```

Check summary statistics:

```python
df.describe()
```

Check missing values:

```python
df.isnull().sum()
```

A good workflow is:

```text
Load data
   ↓
Understand data
   ↓
Check missing values
   ↓
Check data types
   ↓
Explore relationships
   ↓
Build model
```

---

# 5. Define X and y

This is one of the most important steps.

### Features → X

```python
X = df[["experience", "education", "age"]]
```

### Target → y

```python
y = df["salary"]
```

So:

```text
X
├── experience
├── education
└── age

        ↓

    Regression Model

        ↓

y
└── salary
```

### Important

Notice the **double brackets**:

```python
X = df[["experience", "education", "age"]]
```

We use double brackets because `X` contains **multiple columns** and should be a 2D feature matrix.

---

# 6. Split the Data

We shouldn't train and evaluate the model on exactly the same data.

Use `train_test_split()`:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

Here:

```text
Original Data
      │
      ├──────────────► Training Data (80%)
      │
      └──────────────► Testing Data (20%)
```

### Why?

The model learns from the training data.

The test data provides an estimate of how well it performs on **unseen data**.

---

# 7. Create the Regression Model

```python
model = LinearRegression()
```

At this point, the model hasn't learned anything yet.

---

# 8. Train the Model

Use `.fit()`:

```python
model.fit(X_train, y_train)
```

This is where the model estimates the regression coefficients.

Conceptually:

$$
\hat{y}
=
b_0+b_1x_1+b_2x_2+b_3x_3
$$

The model finds coefficients that minimize the sum of squared residuals:

$$
\sum_{i=1}^{n}(y_i-\hat y_i)^2
$$

---

# 9. Get the Intercept

```python
model.intercept_
```

This gives:

$$
b_0
$$

The intercept represents the predicted target when all predictors are zero.

For example, if:

```text
model.intercept_ = 10
```

then:

$$
b_0=10
$$

---

# 10. Get the Coefficients

```python
model.coef_
```

You might get something like:

```text
[5.2, 1.8, 0.7]
```

These correspond to:

```text
experience → 5.2
education  → 1.8
age        → 0.7
```

To make this easier to read:

```python
coefficients = pd.DataFrame({
    "Feature": X.columns,
    "Coefficient": model.coef_
})

coefficients
```

---

# 11. Interpret the Coefficients

Suppose the model is:

$$
\hat{Salary}
=
10
+5.2Experience
+1.8Education
+0.7Age
$$

### Experience

$$
b_1=5.2
$$

Interpretation:

> Holding education and age constant, a one-unit increase in experience is associated with a 5.2-unit increase in predicted salary.

### Education

$$
b_2=1.8
$$

> Holding experience and age constant, a one-unit increase in education is associated with a 1.8-unit increase in predicted salary.

### Age

$$
b_3=0.7
$$

> Holding experience and education constant, a one-unit increase in age is associated with a 0.7-unit increase in predicted salary.

### Important

**"Holding other variables constant"** is extremely important when interpreting multiple regression coefficients.

---

# 12. Make Predictions

Let's predict salary for the test data.

```python
y_pred = model.predict(X_test)
```

Now:

```text
X_test
   ↓
Model
   ↓
y_pred
```

`y_pred` contains the predicted salaries.

---

# 13. Compare Actual vs Predicted

Create a DataFrame:

```python
results = pd.DataFrame({
    "Actual": y_test,
    "Predicted": y_pred
})

results
```

Example:

| Actual | Predicted |
| -----: | --------: |
|     52 |      51.3 |
|     72 |      73.1 |

The closer these values are, generally, the better the predictions.

---

# 14. Calculate Residuals

A residual is:

$$
e_i=y_i-\hat y_i
$$

In Python:

```python
residuals = y_test - y_pred
```

Or:

```python
results["Residual"] = results["Actual"] - results["Predicted"]
```

For example:

```text
Actual     = 70
Predicted  = 67
Residual   = 3
```

The model underestimated by 3.

---

# 15. Calculate \(R^2\)

```python
r2 = r2_score(y_test, y_pred)

print(r2)
```

\(R^2\) measures how much variation in the target is explained by the model relative to a mean-only baseline.

For example:

```text
R² = 0.85
```

means the model explains 85% of the sample variation relative to that baseline, under the usual definition.

### Important

Don't say:

> "The model is 85% accurate."

That's incorrect.

\(R^2\) is **not accuracy**.

---

# 16. Calculate MAE

MAE = Mean Absolute Error.

$$
MAE=
\frac{1}{n}
\sum |y_i-\hat y_i|
$$

Python:

```python
mae = mean_absolute_error(y_test, y_pred)

print(mae)
```

Suppose:

```text
MAE = 3.2
```

This means the predictions are off by about **3.2 salary units on average**, in absolute terms.

---

# 17. Calculate RMSE

RMSE = Root Mean Squared Error.

$$
RMSE=
\sqrt{
\frac{1}{n}
\sum(y_i-\hat y_i)^2
}
$$

Python:

```python
rmse = np.sqrt(
    mean_squared_error(y_test, y_pred)
)

print(rmse)
```

RMSE penalizes large errors more strongly than MAE.

### MAE vs RMSE

| Metric  | Meaning                                       |
| ------- | --------------------------------------------- |
| MAE     | Average absolute prediction error             |
| RMSE    | Error metric that penalizes large errors more |
| \(R^2\) | Explained variation relative to mean baseline |

---

# 18. Predict a New Person's Salary

Suppose we have a new person:

```text
Experience = 7
Education  = 18
Age        = 32
```

Create the input:

```python
new_person = pd.DataFrame({
    "experience": [7],
    "education": [18],
    "age": [32]
})
```

Predict:

```python
prediction = model.predict(new_person)

print(prediction)
```

The model might return:

```text
[67.4]
```

So the predicted salary is approximately:

$$
67.4
$$

---

# 19. Why Column Names Matter

When using a DataFrame, make sure the new data has the same feature names:

```python
new_person = pd.DataFrame({
    "experience": [7],
    "education": [18],
    "age": [32]
})
```

This is safer than:

```python
model.predict([[7, 18, 32]])
```

because the DataFrame makes the feature mapping explicit.

---

# 20. Visualizing Actual vs Predicted

For multiple regression, there isn't usually a simple 2D regression line because there are multiple predictors.

Instead, we can plot actual vs predicted values:

```python
plt.scatter(y_test, y_pred)

plt.xlabel("Actual Salary")
plt.ylabel("Predicted Salary")
plt.title("Actual vs Predicted Salary")

plt.show()
```

Ideally, the points should lie reasonably close to:

$$
y=x
$$

because:

```text
Predicted ≈ Actual
```

---

# 21. Residual Plot

Residual diagnostics are very important.

```python
residuals = y_test - y_pred

plt.scatter(y_pred, residuals)

plt.axhline(0)

plt.xlabel("Predicted Salary")
plt.ylabel("Residual")
plt.title("Residual Plot")

plt.show()
```

Ideally, residuals should be roughly scattered around zero without obvious patterns.

For example:

```text
Residual
   ↑
 + |   .    .   .
 0 |--------------------→ Predicted
 - | .    .     .
```

A strong curve or funnel pattern can indicate problems with the model specification or error assumptions.

---

# 22. Check for Multicollinearity

Multiple regression can have a problem called **multicollinearity**.

Example:

```text
Age ─────────────┐
                 ├── strongly related
Experience ──────┘
```

If predictors are highly correlated, individual coefficients can become unstable and their standard errors can increase.

A common diagnostic is **VIF (Variance Inflation Factor)**.

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

X_vif = X_train.copy()

vif = pd.DataFrame()

vif["Feature"] = X_vif.columns

vif["VIF"] = [
    variance_inflation_factor(X_vif.values, i)
    for i in range(X_vif.shape[1])
]

vif
```

VIF is a diagnostic, not a universal pass/fail rule. Its interpretation depends on context.

---

# 23. Multiple Regression with Categorical Variables

Suppose we add:

```text
Department
-----------
IT
HR
Finance
Sales
```

We can't directly give these text values to ordinary linear regression.

We need to encode them.

Using pandas:

```python
df_encoded = pd.get_dummies(
    df,
    columns=["department"],
    drop_first=True
)
```

This creates indicator variables.

For example:

```text
department_IT
department_HR
department_Sales
```

with one category used as the reference.

---

# 24. Multiple Regression with Train/Test Split

A more realistic complete workflow looks like this:

```python
X = df[["experience", "education", "age"]]
y = df["salary"]

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)

model = LinearRegression()

model.fit(X_train, y_train)

y_pred = model.predict(X_test)

r2 = r2_score(y_test, y_pred)

mae = mean_absolute_error(y_test, y_pred)

rmse = np.sqrt(
    mean_squared_error(y_test, y_pred)
)

print("Intercept:", model.intercept_)
print("Coefficients:", model.coef_)
print("R²:", r2)
print("MAE:", mae)
print("RMSE:", rmse)
```

---

# 25. The Complete Python Workflow

Think of multiple regression as:

```text
             Dataset
                ↓
        Understand Data
                ↓
        Select Features X
                ↓
          Select Target y
                ↓
         Train/Test Split
                ↓
        Create LinearRegression
                ↓
             .fit()
                ↓
           .predict()
                ↓
       ┌────────┼────────┐
       ↓        ↓        ↓
      R²       MAE      RMSE
       │        │        │
       └────────┼────────┘
                ↓
       Residual Diagnostics
                ↓
     Check Model Assumptions
                ↓
       Check Multicollinearity
                ↓
       Improve / Validate Model
```

---

# 26. Important Difference: Training vs Testing

Suppose:

```python
model.fit(X_train, y_train)
```

Then:

```python
train_pred = model.predict(X_train)
test_pred = model.predict(X_test)
```

Evaluate both:

```python
train_r2 = r2_score(y_train, train_pred)
test_r2 = r2_score(y_test, test_pred)

print("Train R²:", train_r2)
print("Test R²:", test_r2)
```

If you get something like:

```text
Train R² = 0.98
Test R²  = 0.62
```

there may be a generalization problem.

The model performs extremely well on training data but considerably worse on unseen data.

---

# 27. Multiple Regression vs Multiple Features in ML

You'll often see:

```python
X = df[["experience", "education", "age"]]
```

This means:

```text
X = Feature Matrix

          experience   education   age
Row 1        1           12        22
Row 2        2           14        24
Row 3        3           14        25
...
```

Conceptually:

$$
X \rightarrow Model \rightarrow y
$$

This same feature-matrix idea is used throughout machine learning.

---

# 28. One Important Point About Feature Scaling

For ordinary `LinearRegression` using OLS, **feature scaling is generally not required** for the model to work.

For example:

```text
Age          → 20–60
Salary       → 30,000–150,000
Experience   → 1–30
```

Different scales do not inherently prevent OLS from fitting the regression.

However, scaling can become useful when using:

* Ridge regression
* Lasso regression
* Elastic Net
* other scale-sensitive algorithms

It can also make coefficient comparisons more meaningful in some contexts.

---

# 29. Common Mistakes

### ❌ Evaluating on training data only

```python
model.fit(X, y)

r2_score(y, model.predict(X))
```

This can give an overly optimistic assessment.

Prefer a proper test set or cross-validation for model evaluation.

---

### ❌ Calling \(R^2\) accuracy

$$
R^2=0.80
$$

doesn't mean:

> "80% accurate."

---

### ❌ Forgetting the other predictors when interpreting a coefficient

In multiple regression:

> Interpret a coefficient conditional on the other included predictors.

---

### ❌ Assuming regression proves causation

Regression finds relationships/associations under a model.

It does not automatically establish cause and effect.

---

### ❌ Ignoring multicollinearity

Highly correlated predictors can make individual coefficient estimates difficult to interpret.

---

### ❌ Using the wrong shape for X

For multiple features:

```python
X = df[["experience", "education", "age"]]
```

not:

```python
X = df["experience"]
```

---

# 🧠 Mental Model

Remember the entire process like this:

```text
Multiple Features
      ↓
     X
      ↓
Linear Regression
      ↓
Coefficients
      ↓
Predictions
      ↓
Compare with Actual Values
      ↓
Evaluate
      ↓
Diagnose
```

Or simply:

> **Prepare → Split → Fit → Predict → Evaluate → Diagnose**

---

# 🎯 Interview-Ready Answer

> **Multiple linear regression is used to predict or model one dependent variable using two or more independent variables. In Python, I typically select the feature matrix X and target y, split the data into training and test sets, fit `LinearRegression()` on the training data, generate predictions on the test data, and evaluate the model using metrics such as R², MAE, and RMSE. I would also examine residuals, multicollinearity, and other relevant assumptions before interpreting the coefficients.**

---

# 📌 Cheat Sheet

```python
# Features and target
X = df[["experience", "education", "age"]]
y = df["salary"]

# Train/test split
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)

# Create model
model = LinearRegression()

# Train
model.fit(X_train, y_train)

# Parameters
model.intercept_
model.coef_

# Predict
y_pred = model.predict(X_test)

# Evaluate
r2_score(y_test, y_pred)

mean_absolute_error(y_test, y_pred)

np.sqrt(mean_squared_error(y_test, y_pred))
```

### One-line takeaway

> **In Python, multiple regression means giving a regression model several features in `X`, fitting the coefficients on training data, predicting the target, and then evaluating and diagnosing how well the model generalizes.**
