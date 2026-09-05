# Using Linear Models for t-tests and ANOVA, Clearly Explained!!!

One of the most useful ideas in statistics is that **t-tests, ANOVA, and linear regression are all closely connected**.

At first, they can look like completely different statistical methods:

```text
t-test  → Compare 2 groups
ANOVA   → Compare 3+ groups
Regression → Model relationship with predictors
```

But underneath, they can all be expressed using the **general linear model**.

---

# 1. The Big Idea

Suppose we want to know whether a treatment changes blood pressure.

We have two groups:

```text
Control      → Blood pressure
Treatment    → Blood pressure
```

A traditional approach would be:

> Run a two-sample t-test.

But we can also represent the same problem as a linear model:

$$
Y=\beta_0+\beta_1X+\epsilon
$$

where:

* \(Y\) = blood pressure
* \(X\) = group indicator
* \(\beta_0\) = mean of the reference group
* \(\beta_1\) = difference between group means
* \(\epsilon\) = unexplained variation

Then testing:

$$
H_0:\beta_1=0
$$

is equivalent to testing whether the two group means are equal.

### Mental model

> **A t-test can be viewed as a simple linear regression with a categorical predictor.**

---

# 2. What Is a Linear Model?

The general form is:

$$
Y=X\beta+\epsilon
$$

For a simple example:

$$
Y=\beta_0+\beta_1X+\epsilon
$$

For multiple regression:

$$
Y=\beta_0+\beta_1X_1+\beta_2X_2+\cdots+\beta_pX_p+\epsilon
$$

The key point is that the predictors can be **numeric or categorical**.

That is what allows us to use the same framework for:

* t-tests
* ANOVA
* regression
* ANCOVA

---

# 3. Two-Group t-test as a Linear Model

Suppose we have:

| Group     | Score |
| --------- | ----: |
| Control   |    70 |
| Control   |    72 |
| Control   |    68 |
| Control   |    71 |
| Treatment |    80 |
| Treatment |    82 |
| Treatment |    78 |
| Treatment |    81 |

We could perform a t-test.

But we can encode the group as:

```text
Control   = 0
Treatment = 1
```

Then our model becomes:

$$
Score=\beta_0+\beta_1Group+\epsilon
$$

---

# 4. What Does the Intercept Mean?

Because:

$$
Group=0
$$

represents Control:

$$
\beta_0=Mean(Control)
$$

Suppose:

$$
\beta_0=70.25
$$

Then the predicted score for Control is:

$$
70.25
$$

---

# 5. What Does the Slope Mean?

For Treatment:

$$
Group=1
$$

Therefore:

$$
Score=\beta_0+\beta_1
$$

So:

$$
\beta_1=Mean(Treatment)-Mean(Control)
$$

Suppose:

$$
\beta_1=10
$$

Then:

$$
Mean(Treatment)=70.25+10=80.25
$$

So the regression coefficient is literally the **difference between group means**.

---

# 6. The t-test Appears Naturally

Our hypothesis is:

$$
H_0:\beta_1=0
$$

versus:

$$
H_1:\beta_1\ne0
$$

The test statistic is:

$$
t=\frac{\hat{\beta}_1}{SE(\hat{\beta}_1)}
$$

This asks:

> How many standard errors away from zero is the estimated group difference?

That's exactly the logic of a two-sample t-test.

---

# 7. The Connection

```text
Two Groups
    ↓
Create a 0/1 group variable
    ↓
Fit Linear Model
    ↓
β₁ = Difference in Group Means
    ↓
Test H₀: β₁ = 0
    ↓
t-test
```

So:

> **Two-group comparison → categorical predictor → linear model → t-test on coefficient**

---

# 8. What About ANOVA?

Now suppose we have **three groups**:

```text
Control
Treatment A
Treatment B
```

A t-test isn't sufficient because there are more than two groups.

We can use:

> **One-way ANOVA**

ANOVA asks:

$$
H_0:
\mu_1=\mu_2=\mu_3
$$

versus:

$$
H_1:
\text{At least one group mean differs}
$$

But we can again represent this as a linear model.

![ANOVA](images/anova.png)

---

# 9. ANOVA as a Linear Model

Suppose:

```text
Group:
A
B
C
```

We create indicator variables.

Choose Group A as the reference.

```text
Group A → Reference

Group B → 0/1
Group C → 0/1
```

The model becomes:

$$
Y=
\beta_0+
\beta_1I(B)+
\beta_2I(C)+
\epsilon
$$

---

# 10. Interpreting the Coefficients

Suppose:

$$
\beta_0=50
$$

$$
\beta_1=10
$$

$$
\beta_2=20
$$

Then:

### Group A

$$
\hat Y=50
$$

### Group B

$$
\hat Y=50+10=60
$$

### Group C

$$
\hat Y=50+20=70
$$

So:

| Group | Predicted Mean |
| ----- | -------------: |
| A     |             50 |
| B     |             60 |
| C     |             70 |

The coefficients represent differences relative to the reference group.

---

# 11. Why Do We Need Multiple Coefficients?

Because there are multiple groups.

With:

```text
A
B
C
```

we need to represent:

```text
B vs A
C vs A
```

So we need two indicator variables.

Generally, with \(k\) categories:

$$
k-1
$$

dummy variables are used when an intercept is included.

---

# 12. What Is the ANOVA F-test?

Instead of testing one coefficient at a time, ANOVA can test the group effect **as a whole**.

The null hypothesis is:

$$
H_0:\beta_1=\beta_2=\cdots=\beta_{k-1}=0
$$

This means:

> None of the groups differ from the reference group.

The ANOVA test uses an F-statistic:

$$
F=
\frac{\text{Between-group variation}}
{\text{Within-group variation}}
$$

More precisely, in the standard one-way ANOVA:

$$
F=\frac{MS_{Between}}{MS_{Within}}
$$

---

# 13. What Does the F-statistic Tell Us?

Think about two scenarios.

### Scenario 1: Groups are similar

```text
A: 49 51 50 52
B: 50 48 51 49
C: 51 50 52 49
```

The group means are close.

Therefore:

```text
Between-group variation ↓
Within-group variation  ↑ relative to between
```

So:

$$
F \approx 1
$$

There isn't strong evidence that the group means differ.

---

### Scenario 2: Groups are very different

```text
A: 48 50 49 51

B: 69 70 71 70

C: 89 91 90 92
```

The group means are far apart.

```text
Between-group variation ↑
Within-group variation ↓ relative to between
```

Therefore:

$$
F\gg1
$$

This provides stronger evidence against equal group means.

---

# 14. The Amazing Connection

We can now see:

```text
                    Linear Model
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
          2 groups     3+ groups    Numeric X
             │           │           │
             ↓           ↓           ↓
          t-test       ANOVA      Regression
```

They are not completely separate worlds.

They can all be represented within the **general linear model framework**.

---

# 15. t-test vs ANOVA

| Feature         | t-test                      | ANOVA                            |
| --------------- | --------------------------- | -------------------------------- |
| Typical groups  | 2                           | 3+                               |
| Linear model    | Yes                         | Yes                              |
| Main test       | t-statistic                 | F-statistic                      |
| Null hypothesis | Difference = 0              | All group means equal            |
| Predictor       | Binary categorical variable | Multi-level categorical variable |

---

# 16. Why Not Just Run Multiple t-tests?

Suppose we have:

```text
A
B
C
D
```

We could run:

```text
A vs B
A vs C
A vs D
B vs C
B vs D
C vs D
```

That's **6 tests**.

The problem is multiple testing.

If you keep testing enough comparisons at \(\alpha=0.05\), the probability of getting at least one false positive increases.

ANOVA gives us an **overall test**:

$$
H_0:\mu_A=\mu_B=\mu_C=\mu_D
$$

before doing individual comparisons.

---

# 17. ANOVA Significant — What Next?

Suppose:

$$
p<0.05
$$

for the ANOVA.

We reject:

$$
H_0:\mu_A=\mu_B=\mu_C
$$

But ANOVA only tells us:

> **At least one group mean differs.**

It doesn't tell us exactly which groups differ.

We can then perform appropriate **post-hoc comparisons**, such as Tukey's HSD, with appropriate multiplicity control.

```text
ANOVA
  ↓
Significant?
  ↓
Yes
  ↓
Post-hoc comparisons
  ↓
Which groups differ?
```

---

# 18. ANOVA Is Really About Variance

Why is it called **Analysis of Variance** if we're comparing means?

Because ANOVA compares two sources of variation:

### Between-group variation

How far group means are from the overall mean.

### Within-group variation

How much observations vary within each group.

```text
Total Variation
      │
      ├── Between-group variation
      │
      └── Within-group variation
```

The F-statistic compares these.

---

# 19. The Sum-of-Squares Decomposition

ANOVA decomposes total variation:

$$
SS_{Total}
=
SS_{Between}
+
SS_{Within}
$$

Where:

* \(SS_{Total}\) = total variation
* \(SS_{Between}\) = variation explained by group differences
* \(SS_{Within}\) = variation remaining within groups

Then:

$$
MS_{Between}
=
\frac{SS_{Between}}{df_{Between}}
$$

and:

$$
MS_{Within}
=
\frac{SS_{Within}}{df_{Within}}
$$

Finally:

$$
F=
\frac{MS_{Between}}{MS_{Within}}
$$

---

# 20. Linear Regression View of ANOVA

Here's the deeper idea.

The ANOVA model:

$$
Y=\text{Group Effect}+\epsilon
$$

is simply a linear model where **Group is represented by categorical predictors**.

So:

```text
ANOVA
  ↓
Categorical Predictor
  ↓
Dummy Variables
  ↓
Linear Model
  ↓
Compare Model Variation
  ↓
F-test
```

---

# 21. Adding Continuous Variables: ANCOVA

Now suppose we compare three groups, but age might also affect the outcome.

Instead of:

$$
Y=Group+\epsilon
$$

we can use:

$$
Y=
\beta_0+
\beta_1Group_B+
\beta_2Group_C+
\beta_3Age+
\epsilon
$$

Now we're doing something commonly called:

> **ANCOVA — Analysis of Covariance**

We're comparing groups while adjusting for a continuous covariate.

This is another example of the flexibility of the linear-model framework.

---

# 22. Multiple Regression + Group Comparison

This connects directly to what you just learned about multiple regression.

Suppose:

$$
Salary=
\beta_0+
\beta_1Experience+
\beta_2Education+
\beta_3Gender+
\epsilon
$$

Here:

* Experience → numerical predictor
* Education → numerical predictor
* Gender → categorical predictor

So a single linear model can contain:

```text
Numerical predictors
        +
Categorical predictors
        ↓
   Linear Model
```

This is why linear models are so powerful.

---

# 23. Python: Two-Group t-test as a Linear Model

Let's create some data:

```python id="d5b4a1"
import pandas as pd
import statsmodels.formula.api as smf

df = pd.DataFrame({
    "group": [
        "Control", "Control", "Control", "Control",
        "Treatment", "Treatment", "Treatment", "Treatment"
    ],
    "score": [
        70, 72, 68, 71,
        80, 82, 78, 81
    ]
})
```

Fit a linear model:

```python id="5n8c2m"
model = smf.ols(
    "score ~ C(group)",
    data=df
).fit()
```

View the results:

```python id="0z7q4n"
print(model.summary())
```

`C(group)` tells `statsmodels` to treat `group` as a categorical variable.

---

# 24. ANOVA in Python

For three groups:

```python id="4v6p2n"
df = pd.DataFrame({
    "group": [
        "A", "A", "A", "A",
        "B", "B", "B", "B",
        "C", "C", "C", "C"
    ],
    "score": [
        48, 50, 49, 51,
        59, 61, 60, 62,
        69, 71, 70, 72
    ]
})
```

Fit the linear model:

```python id="b0c8yu"
model = smf.ols(
    "score ~ C(group)",
    data=df
).fit()
```

Then run ANOVA:

```python id="q8u4em"
from statsmodels.stats.anova import anova_lm

anova_table = anova_lm(model)

print(anova_table)
```

You'll get an ANOVA table containing things such as:

```text
sum_sq
df
F
PR(>F)
```

The `PR(>F)` column is the ANOVA p-value.

---

# 25. The Most Important Connection

You can think of the methods like this:

```text
                 GENERAL LINEAR MODEL
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ↓                ↓                ↓
   Binary Group      Multi-level       Numeric
     Predictor         Group          Predictor
        │                │                │
        ↓                ↓                ↓
     t-test            ANOVA        Regression
```

And you can combine them:

```text
Numeric + Categorical Predictors
              ↓
       Multiple Linear Model
              ↓
      t-tests + F-tests
```

---

# 26. t-test vs F-test

There is an especially important mathematical relationship.

When testing **one restriction**, the statistics are related by:

$$
F=t^2
$$

For example, if:

$$
t=2
$$

then:

$$
F=4
$$

with the corresponding degrees of freedom relationship in the standard nested linear-model setting.

So the t-test and F-test are not unrelated tests.

---

# 27. Coefficient Test vs Overall Model Test

Suppose:

$$
Y=\beta_0+\beta_1X_1+\beta_2X_2+\beta_3X_3+\epsilon
$$

We could test one coefficient:

$$
H_0:\beta_1=0
$$

using a **t-test**.

Or we could test multiple coefficients simultaneously:

$$
H_0:\beta_1=\beta_2=\beta_3=0
$$

using an **F-test**.

This is a very important distinction.

```text
One coefficient
      ↓
    t-test

Several coefficients / restrictions
      ↓
    F-test
```

---

# 28. Why This Matters in Data Science

Instead of learning:

```text
t-test
ANOVA
regression
ANCOVA
```

as completely separate techniques, you can learn the underlying framework:

> **Linear models provide one common language for many of these methods.**

This makes it much easier to move from classical statistics to statistical modeling.

---

# 29. The Bigger Picture

```text
                         Linear Model
                              │
                ┌─────────────┼─────────────┐
                ↓             ↓             ↓
          Numeric X      Binary X       Categorical X
                │             │             │
                ↓             ↓             ↓
           Regression      t-test         ANOVA
                                             │
                                             ↓
                                      3+ group means
                                             │
                                             ↓
                                       F-test
                                             │
                              ┌──────────────┴─────────────┐
                              ↓                            ↓
                       Significant?                   Not significant
                              ↓                            ↓
                     Post-hoc tests                  Stop / interpret
```

---

# 🧠 Mental Model

Remember this:

> **A t-test is basically a linear model with a two-level categorical predictor. ANOVA is a linear model with a multi-level categorical predictor. Regression uses numerical predictors.**

The same linear-model machinery can handle all of them.

---

# 🎯 Interview-Ready Answer

> **t-tests and ANOVA can be expressed as special cases of the general linear model. A two-group t-test can be represented as a linear regression with a binary categorical predictor, where the coefficient represents the difference between the two group means. ANOVA extends this idea to a categorical predictor with three or more levels, typically using dummy variables. The overall group effect is tested using an F-test, while individual coefficients can be tested using t-tests. This unified framework also allows us to combine categorical and continuous predictors, as in ANCOVA and multiple regression.**

---

## One-Line Takeaway

> **t-tests, ANOVA, and regression are different applications of the same linear-model framework: encode predictors appropriately, fit the model, and use t-tests or F-tests to test the relevant coefficients or groups.**
