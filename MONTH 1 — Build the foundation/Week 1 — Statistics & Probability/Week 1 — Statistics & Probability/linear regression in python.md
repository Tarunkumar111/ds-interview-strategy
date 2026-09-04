# Linear Regression in Python, Step-by-Step

Let's build a **simple linear regression model from scratch**, understand what each step does, and then use `scikit-learn` to do the same thing efficiently.

We'll use a simple example:

> **Predict salary based on years of experience.**

---

## 1. Import the Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
```

We'll use:

* **NumPy** → numerical calculations
* **Pandas** → data handling
* **Matplotlib** → visualization
* **scikit-learn** → linear regression and evaluation

---

# 2. Create Some Data

```python
data = {
    "experience": [1, 2, 3, 4, 5, 6, 7, 8],
    "salary": [30, 35, 40, 45, 50, 58, 62, 70]
}

df = pd.DataFrame(data)

df
```

Output:

```text
   experience  salary
0           1      30
1           2      35
2           3      40
3           4      45
4           5      50
5           6      58
6           7      62
7           8      70
```

Here:

$$
X=\text{experience}
$$

and:

$$
Y=\text{salary}
$$

---

# 3. Understand the Data

Before fitting a model, visualize the relationship.

```python
plt.scatter(df["experience"], df["salary"])

plt.xlabel("Years of Experience")
plt.ylabel("Salary")
plt.title("Experience vs Salary")

plt.show()
```

You should see an approximately upward trend.

```text
Salary
  |
70|              •
60|           •
50|       •  •
40|     •
30| •  •
  +--------------------
    1 2 3 4 5 6 7 8
       Experience
```

This suggests that a linear model may be reasonable.

---

# 4. Define X and y

Separate the **predictor** and **target**.

```python
X = df[["experience"]]
y = df["salary"]
```

Notice the double brackets:

```python
df[["experience"]]
```

This creates a **2D DataFrame**, which is the expected shape for scikit-learn features.

While:

```python
df["experience"]
```

is a 1D Series.

### Shapes

```python
print(X.shape)
print(y.shape)
```

Output:

```text
(8, 1)
(8,)
```

Think:

```text
X → Features / Predictors
y → Target / Outcome
```

---

# 5. Create the Linear Regression Model

```python
model = LinearRegression()
```

At this point, we have created the model object.

But we haven't trained it yet.

```text
LinearRegression()
       ↓
Model exists
       ↓
Not trained yet
```

---

# 6. Fit the Model

Now train the model:

```python
model.fit(X, y)
```

This is the important step.

The model finds the coefficients that minimize the **sum of squared residuals**:

$$
\boxed{
\sum_{i=1}^{n}(y_i-\hat y_i)^2
}
$$

Conceptually:

```text
Data
 ↓
Try possible line
 ↓
Calculate residuals
 ↓
Square residuals
 ↓
Minimize total
 ↓
Best-fitting line
```

---

# 7. Get the Intercept

```python
model.intercept_
```

Suppose Python gives:

```text
21.07
```

Then:

$$
b_0\approx21.07
$$

This is the estimated value of salary when experience is zero.

---

# 8. Get the Slope

```python
model.coef_
```

Suppose we get:

```text
array([5.86])
```

Then:

$$
b_1\approx5.86
$$

So the fitted model is approximately:

$$
\boxed{
\hat y=21.07+5.86x
}
$$

---

# 9. Interpret the Model

The slope is:

$$
5.86
$$

So:

> For each additional year of experience, the model predicts an approximately 5.86-unit increase in salary.

The intercept is:

$$
21.07
$$

So:

> When experience is zero, the model predicts a salary of approximately 21.07 units.

Remember that the intercept may not have a meaningful real-world interpretation if \(X=0\) is outside the relevant range.

---

# 10. Make Predictions

Suppose we want to predict the salary for someone with:

$$
10
$$

years of experience.

```python
new_data = pd.DataFrame({
    "experience": [10]
})

prediction = model.predict(new_data)

print(prediction)
```

The model calculates:

$$
\hat y=b_0+b_1(10)
$$

Using our approximate coefficients:

$$
\hat y=21.07+5.86(10)
$$

$$
\approx79.67
$$

So the predicted salary is approximately:

$$
\boxed{79.67}
$$

---

# 11. Predict All Training Observations

We can generate predictions for the original data:

```python
df["predicted_salary"] = model.predict(X)

df
```

Now we'll have something like:

```text
   experience  salary  predicted_salary
0           1      30             26.93
1           2      35             32.79
2           3      40             38.65
...
```

These are the values predicted by the fitted regression line.

---

# 12. Calculate Residuals

Remember:

$$
\boxed{
e_i=y_i-\hat y_i
}
$$

In Python:

```python
df["residual"] = df["salary"] - df["predicted_salary"]
```

Now:

```text
Actual
   ↓
Predicted
   ↓
Residual
```

For example:

```text
Actual salary     = 40
Predicted salary  = 38.65

Residual = 40 - 38.65
         = 1.35
```

---

# 13. Plot the Regression Line

```python
plt.scatter(X, y, label="Actual")

plt.plot(
    X,
    model.predict(X),
    label="Regression Line"
)

plt.xlabel("Years of Experience")
plt.ylabel("Salary")
plt.title("Linear Regression")

plt.legend()
plt.show()
```

You'll see:

```text
Salary
  |
70|                 •
60|             •  /
50|          •   /
40|       •    /
30|   •  /   •
  |  /
  +------------------- Experience
```

The dots are the actual observations.

The line is the fitted regression model.

---

# 14. Calculate R-squared

Now we can evaluate how much variation the model explains.

```python
r2 = model.score(X, y)

print(r2)
```

Or explicitly:

```python
predictions = model.predict(X)

r2 = r2_score(y, predictions)

print(r2)
```

Suppose:

```text
R² = 0.98
```

We can say:

> The model explains approximately 98% of the variation in salary in this dataset, relative to a mean-only baseline.

### Important

Don't say:

> "The model is 98% accurate."

That's not what \(R^2\) means.

---

# 15. Calculate MAE

**Mean Absolute Error** measures the average absolute prediction error.

$$
\boxed{
MAE=\frac{1}{n}\sum|y_i-\hat y_i|
}
$$

Python:

```python
mae = mean_absolute_error(y, predictions)

print(mae)
```

Suppose:

```text
MAE = 1.8
```

That means the predictions are off by about 1.8 salary units on average, in absolute terms.

---

# 16. Calculate RMSE

**Root Mean Squared Error** is:

$$
\boxed{
RMSE=
\sqrt{
\frac{1}{n}
\sum(y_i-\hat y_i)^2
}
}
$$

Python:

```python
rmse = np.sqrt(mean_squared_error(y, predictions))

print(rmse)
```

RMSE gives more weight to larger errors because the errors are squared before taking the square root.

---

# 17. MAE vs RMSE

| Metric | Meaning                                         |
| ------ | ----------------------------------------------- |
| MAE    | Average absolute prediction error               |
| RMSE   | Square-root of average squared prediction error |
| R²     | Variation explained relative to mean baseline   |

### Mental model

```text
MAE
 ↓
Average size of errors

RMSE
 ↓
Average error with larger errors penalized more

R²
 ↓
How much variation is explained
```

---

# 18. Don't Evaluate Only on Training Data

This is **very important** in machine learning.

So far we've:

```text
Data
 ↓
Fit model
 ↓
Evaluate same data
```

That's training performance.

It can be overly optimistic, particularly with flexible models.

Instead, we usually split the data.

---

# 19. Train-Test Split

```python
from sklearn.model_selection import train_test_split
```

Then:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

Now we have:

```text
Original Data
     │
     ├──────────────┐
     ↓              ↓
Training Data    Test Data
     │              │
     ↓              │
Train model         │
     │              │
     └──────┬───────┘
            ↓
       Evaluate on
       unseen data
```

---

# 20. Fit Using Training Data

```python
model = LinearRegression()

model.fit(X_train, y_train)
```

Notice:

> We fit the model using **only the training data**.

---

# 21. Predict the Test Data

```python
y_pred = model.predict(X_test)
```

Now compare:

```text
y_test
   ↓
Actual unseen values

y_pred
   ↓
Model predictions
```

---

# 22. Evaluate Test Performance

### Test R²

```python
r2 = r2_score(y_test, y_pred)

print("Test R²:", r2)
```

### Test MAE

```python
mae = mean_absolute_error(y_test, y_pred)

print("Test MAE:", mae)
```

### Test RMSE

```python
rmse = np.sqrt(mean_squared_error(y_test, y_pred))

print("Test RMSE:", rmse)
```

Now we're measuring how the model performs on **data it didn't train on**.

---

# 23. Complete Example

Here's the complete basic workflow:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score


# 1. Create data
data = {
    "experience": [1, 2, 3, 4, 5, 6, 7, 8],
    "salary": [30, 35, 40, 45, 50, 58, 62, 70]
}

df = pd.DataFrame(data)


# 2. Define features and target
X = df[["experience"]]
y = df["salary"]


# 3. Split data
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)


# 4. Create model
model = LinearRegression()


# 5. Train model
model.fit(X_train, y_train)


# 6. Make predictions
y_pred = model.predict(X_test)


# 7. Model coefficients
print("Intercept:", model.intercept_)
print("Slope:", model.coef_[0])


# 8. Evaluate model
print("R²:", r2_score(y_test, y_pred))
print("MAE:", mean_absolute_error(y_test, y_pred))
print("RMSE:", np.sqrt(mean_squared_error(y_test, y_pred)))


# 9. Plot
plt.scatter(X, y)

plt.plot(
    X,
    model.predict(X)
)

plt.xlabel("Years of Experience")
plt.ylabel("Salary")
plt.title("Linear Regression")

plt.show()
```

---

# 24. What Is Happening Under the Hood?

When you call:

```python
model.fit(X, y)
```

OLS is essentially trying to find:

$$
b_0,b_1
$$

that minimize:

$$
\boxed{
\sum_{i=1}^{n}
(y_i-(b_0+b_1x_i))^2
}
$$

Then the fitted model becomes:

$$
\boxed{
\hat y=b_0+b_1x
}
$$

So:

```text
X
↓
Linear model
↓
b₀ + b₁X
↓
Predictions
↓
Residuals
↓
Squared residuals
↓
Minimize
↓
Best coefficients
```

---

# 25. Multiple Linear Regression in Python

Now suppose salary depends on multiple variables:

* experience
* education
* age

Then:

```python
X = df[[
    "experience",
    "education",
    "age"
]]

y = df["salary"]

model = LinearRegression()

model.fit(X, y)
```

The model becomes:

$$
\boxed{
\hat y=
b_0+
b_1x_1+
b_2x_2+
b_3x_3
}
$$

You can inspect the coefficients:

```python
print(model.intercept_)
print(model.coef_)
```

---

# 26. Interpreting Multiple Regression

Suppose:

```text
experience coefficient = 5
education coefficient  = 3
age coefficient         = -1
```

Then, approximately:

### Experience

> Holding the other included predictors constant, a one-unit increase in experience is associated with a 5-unit increase in predicted salary.

### Education

> Holding the other included predictors constant, a one-unit increase in education is associated with a 3-unit increase in predicted salary.

### Age

> Holding the other included predictors constant, a one-unit increase in age is associated with a 1-unit decrease in predicted salary.

Again, these are **associations**, not automatically causal effects.

---

# 27. A Better Real-World Workflow

For a real dataset, don't jump straight to:

```python
model.fit(X, y)
```

A better workflow is:

```text
Load data
   ↓
Understand data
   ↓
Clean data
   ↓
Explore relationships
   ↓
Choose features
   ↓
Split train/test
   ↓
Fit model
   ↓
Make predictions
   ↓
Evaluate
   ↓
Check residuals
   ↓
Validate assumptions
   ↓
Improve model
```

---

# 28. What to Check After Fitting?

Don't rely only on \(R^2\).

Check:

### 1. Residuals

```python
residuals = y_test - y_pred
```

### 2. MAE

```python
mean_absolute_error(y_test, y_pred)
```

### 3. RMSE

```python
np.sqrt(mean_squared_error(y_test, y_pred))
```

### 4. R²

```python
r2_score(y_test, y_pred)
```

### 5. Residual plot

Look for systematic patterns.

```text
Good:

Residual
  |
 +| •   •   •
  |    •
  | •     •
 -|    •
  +------------- X
```

A curved or funnel-shaped pattern can indicate that the model assumptions or specification need attention.

---

# 29. Common Mistakes in Python

### ❌ Mistake 1: Wrong shape for X

This:

```python
X = df["experience"]
```

is a 1D Series.

Often preferable for scikit-learn:

```python
X = df[["experience"]]
```

which is 2D.

---

### ❌ Mistake 2: Training and testing on the same data

Avoid evaluating only:

```python
model.fit(X, y)
model.predict(X)
```

for an honest estimate of generalization.

Use a train/test split or cross-validation.

---

### ❌ Mistake 3: Saying R² is accuracy

$$
R^2\neq\text{accuracy}
$$

---

### ❌ Mistake 4: Ignoring residuals

A high \(R^2\) doesn't guarantee that the model is appropriate.

---

### ❌ Mistake 5: Assuming correlation means causation

A regression coefficient showing association doesn't automatically establish a causal relationship.

---

### ❌ Mistake 6: Extrapolating blindly

If your training data contain:

$$
X=1\text{ to }10
$$

be careful about predicting at:

$$
X=100
$$

The relationship may not continue outside the observed range.

---

# 30. Linear Regression Cheat Sheet

```python
# Create model
model = LinearRegression()

# Train
model.fit(X_train, y_train)

# Predict
y_pred = model.predict(X_test)

# Intercept
model.intercept_

# Coefficients
model.coef_

# R²
r2_score(y_test, y_pred)

# MAE
mean_absolute_error(y_test, y_pred)

# RMSE
np.sqrt(mean_squared_error(y_test, y_pred))
```

---

# 31. The Complete Mental Model

```text
              DATA
                ↓
       Features X + Target y
                ↓
          Train / Test Split
                ↓
         LinearRegression()
                ↓
            model.fit()
                ↓
        Find b₀, b₁, ...
                ↓
       ŷ = b₀ + b₁X + ...
                ↓
          model.predict()
                ↓
         ┌──────┼───────┐
         ↓      ↓       ↓
        R²     MAE     RMSE
         │      │       │
         └──────┼───────┘
                ↓
       Check residuals +
       model assumptions
                ↓
       Generalization / Use
```

# 🧠 Interview-Ready Answer

> **To perform linear regression in Python, I first prepare the features \(X\) and target \(y\), split the data into training and test sets, create a `LinearRegression` model from scikit-learn, and fit it using the training data. I then use `predict()` to generate predictions on the test set and evaluate performance using metrics such as R², MAE, and RMSE. I also inspect residuals and model assumptions rather than relying on R² alone.**

### One-line takeaway

$$
\boxed{
\text{Prepare data}
\rightarrow
\text{Split}
\rightarrow
\text{Fit}
\rightarrow
\text{Predict}
\rightarrow
\text{Evaluate}
\rightarrow
\text{Diagnose}
}
$$

**The key Python commands to remember:**

```python
model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

That is the core of doing linear regression with `scikit-learn`.
