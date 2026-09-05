# Design Matrices for Linear Models, Clearly Explained!!!

A **design matrix** is simply the way we organize our predictor variables into a matrix so that a linear model can use them.

It sounds complicated, but the core idea is surprisingly simple:

> **The design matrix \(X\) is a structured table of predictor information that tells the linear model what variables to use for each observation.**

Once you understand design matrices, **linear regression, multiple regression, t-tests, ANOVA, and categorical variables** become much easier to connect.

---

# 1. Start With Simple Linear Regression

Suppose we have:

| Experience | Salary |
| ---------: | -----: |
|          1 |     30 |
|          2 |     35 |
|          3 |     40 |
|          4 |     45 |

Our model is:

$$
y=\beta_0+\beta_1x+\epsilon
$$

For example:

$$
Salary=\beta_0+\beta_1Experience+\epsilon
$$

We can write this in matrix form:

$$
\mathbf y=\mathbf X\boldsymbol\beta+\boldsymbol\epsilon
$$

The design matrix is:

$$
X=
\begin{bmatrix}
1&1\\
1&2\\
1&3\\
1&4
\end{bmatrix}
$$

Notice the first column of **1s**.

That's the intercept column.

---

# 2. Why Do We Need the Column of 1s?

Our equation is:

$$
y=\beta_0+\beta_1x
$$

We can rewrite it as:

$$
y=\beta_0(1)+\beta_1x
$$

Now look at the matrix:

$$
X=
\begin{bmatrix}
1&1\\
1&2\\
1&3\\
1&4
\end{bmatrix}
$$

The columns represent:

```text
Column 1 → Intercept
Column 2 → Experience
```

And:

$$
\beta=
\begin{bmatrix}
\beta_0\\
\beta_1
\end{bmatrix}
$$

So:

$$
X\beta
$$

produces the predicted values.

---

# 3. Let's See One Row

Take the first observation:

$$
[1,\ 1]
$$

Multiply it by:

$$
\begin{bmatrix}
\beta_0\\
\beta_1
\end{bmatrix}
$$

We get:

$$
1(\beta_0)+1(\beta_1)
$$

which is:

$$
\beta_0+\beta_1
$$

That's exactly the regression equation for someone with one year of experience.

For the fourth observation:

$$
[1,\ 4]
$$

we get:

$$
1(\beta_0)+4(\beta_1)
$$

$$
=\beta_0+4\beta_1
$$

That's the predicted salary for someone with four years of experience.

---

# 4. Multiple Regression

Now suppose we have:

* Experience
* Education
* Age

Our model is:

$$
y=
\beta_0+
\beta_1Experience+
\beta_2Education+
\beta_3Age+
\epsilon
$$

The design matrix becomes:

$$
X=
\begin{bmatrix}
1&x_{11}&x_{12}&x_{13}\\
1&x_{21}&x_{22}&x_{23}\\
1&x_{31}&x_{32}&x_{33}\\
\vdots&\vdots&\vdots&\vdots\\
1&x_{n1}&x_{n2}&x_{n3}
\end{bmatrix}
$$

For example:

| Intercept | Experience | Education | Age |
| --------: | ---------: | --------: | --: |
|         1 |          2 |        12 |  24 |
|         1 |          4 |        16 |  28 |
|         1 |          6 |        16 |  32 |
|         1 |          8 |        18 |  36 |

So:

```text
X
│
├── Column 1 → Intercept
├── Column 2 → Experience
├── Column 3 → Education
└── Column 4 → Age
```

---

# 5. The Coefficient Vector

Our coefficients are:

$$
\beta=
\begin{bmatrix}
\beta_0\\
\beta_1\\
\beta_2\\
\beta_3
\end{bmatrix}
$$

Therefore:

$$
X\beta
$$

produces:

$$
\begin{bmatrix}
\hat y_1\\
\hat y_2\\
\hat y_3\\
\vdots\\
\hat y_n
\end{bmatrix}
$$

In other words:

```text
Design Matrix X
       ↓
   Coefficients β
       ↓
    Xβ = Predictions
```

---

# 6. The Most Important Structure

Think of a design matrix as:

> **Rows = observations**

> **Columns = predictors/features**

For example:

$$
X=
\begin{bmatrix}
1&2&12&24\\
1&4&16&28\\
1&6&16&32\\
1&8&18&36
\end{bmatrix}
$$

There are:

* 4 observations → 4 rows
* 3 predictors + intercept → 4 columns

So:

$$
X \text{ has shape }(4,4)
$$

---

# 7. Design Matrix in Python

Using pandas:

```python id="h4xj7k"
import pandas as pd

df = pd.DataFrame({
    "experience": [2, 4, 6, 8],
    "education": [12, 16, 16, 18],
    "age": [24, 28, 32, 36],
    "salary": [35, 50, 65, 80]
})
```

The predictors are:

```python id="zq5k3v"
X = df[["experience", "education", "age"]]
```

Conceptually, the design matrix with an intercept is:

```text
     intercept  experience  education  age
0       1           2          12      24
1       1           4          16      28
2       1           6          16      32
3       1           8          18      36
```

---

# 8. Important: scikit-learn Handles the Intercept

With:

```python id="7d5n6p"
from sklearn.linear_model import LinearRegression

model = LinearRegression()

model.fit(X, df["salary"])
```

you normally **don't manually add a column of 1s**.

`LinearRegression()` includes an intercept by default.

So internally, conceptually, it handles something like:

```text
[1, experience, education, age]
```

If you use:

```python id="e4m6sy"
LinearRegression(fit_intercept=False)
```

then the model does **not** fit an intercept, so you would need to handle the design appropriately yourself.

---

# 9. Design Matrix for a t-test

Now the really interesting part.

Suppose we compare:

```text
Control
Treatment
```

We encode:

```text
Control   = 0
Treatment = 1
```

Our design matrix becomes:

$$
X=
\begin{bmatrix}
1&0\\
1&0\\
1&0\\
1&1\\
1&1\\
1&1
\end{bmatrix}
$$

The columns are:

```text
Column 1 → Intercept
Column 2 → Treatment indicator
```

Our model is:

$$
Y=\beta_0+\beta_1Treatment+\epsilon
$$

---

# 10. What Do the Coefficients Mean?

Because Control = 0:

$$
\beta_0=Mean(Control)
$$

And because Treatment = 1:

$$
\beta_0+\beta_1=Mean(Treatment)
$$

Therefore:

$$
\beta_1=
Mean(Treatment)-Mean(Control)
$$

This is why a two-group t-test can be represented using a linear model.

```text
Two Groups
    ↓
0/1 Indicator
    ↓
Design Matrix
    ↓
Linear Model
    ↓
β₁ = Difference in Means
    ↓
t-test
```

---

# 11. Design Matrix for ANOVA

Now suppose we have three groups:

```text
A
B
C
```

We choose A as the reference group.

Then create two indicator variables:

```text
B_indicator
C_indicator
```

The design matrix looks like:

| Intercept |  B |  C |
| --------: | -: | -: |
|         1 |  0 |  0 |
|         1 |  0 |  0 |
|         1 |  1 |  0 |
|         1 |  1 |  0 |
|         1 |  0 |  1 |
|         1 |  0 |  1 |

The model is:

$$
Y=
\beta_0+
\beta_1B+
\beta_2C+
\epsilon
$$

---

# 12. Interpreting This ANOVA Design Matrix

Because A is the reference:

$$
\beta_0=Mean(A)
$$

$$
\beta_1=Mean(B)-Mean(A)
$$

$$
\beta_2=Mean(C)-Mean(A)
$$

So:

```text
β₀ → Group A mean

β₁ → B − A

β₂ → C − A
```

This is how categorical variables become usable in linear models.

---

# 13. Why \(k-1\) Dummy Variables?

Suppose there are \(k\) groups.

With an intercept, we usually use:

$$
k-1
$$

dummy variables.

For three groups:

```text
A
B
C
```

we need:

```text
B indicator
C indicator
```

A is represented when both are zero.

---

# 14. Why Not Use All Three Dummy Variables?

Suppose we tried:

|  A |  B |  C |
| -: | -: | -: |
|  1 |  0 |  0 |
|  0 |  1 |  0 |
|  0 |  0 |  1 |

and also included an intercept:

| Intercept |  A |  B |  C |
| --------: | -: | -: | -: |
|         1 |  1 |  0 |  0 |
|         1 |  0 |  1 |  0 |
|         1 |  0 |  0 |  1 |

Notice:

$$
Intercept=A+B+C
$$

There is perfect linear dependence between the columns.

This is called **perfect multicollinearity** or the **dummy-variable trap**.

The model cannot uniquely estimate all those coefficients.

So we typically remove one category or remove the intercept.

---

# 15. Design Matrix and Categorical Variables

This gives us a general principle:

> **Categorical variables need to be represented numerically in the design matrix.**

For example:

```text
Department
    ↓
IT / HR / Finance
    ↓
Dummy / indicator variables
    ↓
Design Matrix
    ↓
Linear Model
```

---

# 16. Design Matrix with Numeric + Categorical Predictors

Suppose our model is:

$$
Salary=
\beta_0+
\beta_1Experience+
\beta_2Age+
\beta_3Master+
\beta_4PhD+
\epsilon
$$

where Bachelor's degree is the reference category.

Our design matrix might look like:

| Intercept | Experience | Age | Master | PhD |
| --------: | ---------: | --: | -----: | --: |
|         1 |          2 |  24 |      0 |   0 |
|         1 |          4 |  28 |      1 |   0 |
|         1 |          6 |  32 |      0 |   1 |
|         1 |          8 |  36 |      1 |   0 |

Now we can combine:

* numerical predictors
* categorical predictors
* interactions
* transformations

inside the same design matrix.

---

# 17. Interaction Terms in the Design Matrix

Suppose we want:

$$
Y=
\beta_0+
\beta_1X+
\beta_2Group+
\beta_3(X\times Group)
+\epsilon
$$

We simply add another column:

```text
Intercept   X   Group   X×Group
    1       2     0        0
    1       4     0        0
    1       3     1        3
    1       5     1        5
```

The design matrix contains the interaction as another predictor column.

That's an important insight:

> **An interaction is not a completely different kind of model. It's another column in the design matrix.**

---

# 18. Polynomial Regression

Suppose we want:

$$
Y=
\beta_0+
\beta_1X+
\beta_2X^2+
\epsilon
$$

The design matrix becomes:

| Intercept |  X | \(X^2\) |
| --------: | -: | ------: |
|         1 |  1 |       1 |
|         1 |  2 |       4 |
|         1 |  3 |       9 |
|         1 |  4 |      16 |

Notice something interesting:

The relationship with \(X\) is curved, but the model is still **linear in its coefficients**:

$$
\beta_0,\beta_1,\beta_2
$$

That's why polynomial regression is still considered a linear model in the parameters.

---

# 19. The Design Matrix Is More General Than a "Feature Table"

A useful way to think about it:

```text
Feature Table
      ↓
Transform / Encode
      ↓
Design Matrix
      ↓
Linear Model
```

The design matrix doesn't necessarily contain the raw variables.

It can contain:

* raw numerical variables
* dummy variables
* interactions
* polynomial terms
* transformed variables
* spline basis functions

---

# 20. Design Matrix and OLS

Once we have:

$$
Y=X\beta+\epsilon
$$

OLS estimates \(\beta\) by minimizing:

$$
\|Y-X\beta\|^2
$$

Under the usual full-rank assumptions, the OLS solution is:

$$
\hat{\beta}
=
(X^TX)^{-1}X^TY
$$

This equation is the mathematical heart of ordinary least squares.

### Important

You don't normally need to calculate this manually.

Libraries such as `scikit-learn` and `statsmodels` handle the computation.

---

# 21. Why the Matrix Formula Makes Sense

Remember:

$$
X\beta
$$

represents the model's predictions.

Therefore:

$$
Y-X\beta
$$

represents the residuals.

So OLS asks:

> Which coefficients make the residuals as small as possible in squared terms?

$$
\min_\beta
\|Y-X\beta\|^2
$$

That's the matrix version of:

$$
\min_\beta
\sum_i(y_i-\hat y_i)^2
$$

Same idea—just compact notation.

---

# 22. Design Matrix Dimensions

Suppose we have:

* \(n=100\) observations
* \(p=3\) predictors
* an intercept

Then:

$$
X\text{ has shape }(100,4)
$$

because:

```text
100 rows
  ↓
100 observations

4 columns
  ↓
1 intercept
+
3 predictors
```

The coefficient vector has shape:

$$
\beta=(4,1)
$$

And:

$$
X\beta
$$

has shape:

$$
(100,1)
$$

which gives one prediction per observation.

---

# 23. Design Matrix in `statsmodels`

`statsmodels` makes the idea particularly visible.

```python id="v83qmf"
import statsmodels.formula.api as smf

model = smf.ols(
    "salary ~ experience + education + age",
    data=df
).fit()
```

The formula:

```text
salary ~ experience + education + age
```

essentially tells `statsmodels` to construct a design matrix containing:

```text
Intercept
Experience
Education
Age
```

For categorical variables:

```python id="k0fn5p"
model = smf.ols(
    "salary ~ experience + C(department)",
    data=df
).fit()
```

`C(department)` tells `statsmodels` that `department` should be treated as categorical.

---

# 24. Design Matrix and t-tests / ANOVA

Now you can see the complete connection:

### t-test

```text
Group
 ↓
0/1 encoding
 ↓
Design Matrix
 ↓
Linear Model
 ↓
Coefficient t-test
```

### ANOVA

```text
Group
 ↓
Dummy variables
 ↓
Design Matrix
 ↓
Linear Model
 ↓
Overall F-test
```

### Multiple regression

```text
Multiple predictors
 ↓
Design Matrix
 ↓
Linear Model
 ↓
Coefficient tests / predictions
```

They're all using the same underlying machinery.

---

# 25. One Design Matrix Can Represent Many Models

Consider:

$$
X=
\begin{bmatrix}
1&2&12&24\\
1&4&16&28\\
1&6&16&32\\
1&8&18&36
\end{bmatrix}
$$

This matrix says:

```text
Column 1 → intercept
Column 2 → experience
Column 3 → education
Column 4 → age
```

The model then determines how these columns combine to predict \(Y\).

This is why the design matrix is such a fundamental concept.

---

# 26. Common Mistakes

### ❌ "Design matrix is just the raw dataset."

Not necessarily.

It is the **model-ready representation of predictors**.

It can contain transformed and encoded variables.

---

### ❌ "Rows are variables."

Usually the opposite:

> **Rows = observations**

> **Columns = predictors/model terms**

---

### ❌ "The intercept is automatically a real feature."

No.

The intercept is represented by a column of ones when the model includes one.

---

### ❌ "Categorical variables can't be used in linear regression."

They can.

They need an appropriate encoding in the design matrix.

---

### ❌ "ANOVA and regression use completely different mathematics."

They can be represented using the same linear-model framework.

---

# 🧠 Mental Model

The easiest way to remember a design matrix:

> **Take every observation, turn all the variables/model terms into columns, add an intercept column if needed, and put everything into a matrix that the linear model can operate on.**

Think:

```text
Raw Data
   ↓
Choose variables
   ↓
Encode categories
   ↓
Create transformations/interactions
   ↓
Design Matrix X
   ↓
Estimate β
   ↓
Predictions + statistical tests
```

---

# 🎯 Interview-Ready Answer

> **A design matrix is a matrix representation of the predictors or model terms used in a linear model. Each row typically represents an observation, and each column represents a predictor, an intercept, or another model term such as a dummy variable, interaction, or polynomial term. For example, in multiple regression with an intercept and three predictors, the design matrix has four columns: a column of ones for the intercept and one column for each predictor. Design matrices provide a common framework for linear regression, t-tests, ANOVA, and models containing categorical variables.**

---

# 🔑 One-Line Takeaway

> **The design matrix \(X\) is the model-ready table of predictors—rows are observations, columns are model terms—and it is the foundation that lets linear models handle regression, t-tests, ANOVA, categorical variables, and interactions in one unified framework.**
