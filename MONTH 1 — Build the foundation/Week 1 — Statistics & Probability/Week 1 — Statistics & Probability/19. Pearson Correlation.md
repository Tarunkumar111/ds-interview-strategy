# Pearson's Correlation, Clearly Explained!!!

## 1. What is Pearson's Correlation?

**Pearson's correlation coefficient** measures the **strength and direction of a linear relationship between two numerical variables**.

It is represented by:

$$
\boxed{r}
$$

Its value always lies between:

$$
\boxed{-1 \le r \le +1}
$$

In simple words:

> **Pearson correlation tells us how strongly two variables tend to move together in a linear way.**

![Negative Correlation](images/negative_correlation.png)

![Zero Correlation](images/zero_correlation.png)

![Positive Correlation](images/positive_correlation.png)

---

# 2. Understanding the Values of \(r\)

The value of \(r\) tells us both **direction** and **strength**.

| Pearson \(r\) | Interpretation                       |
| ------------: | ------------------------------------ |
|        \(+1\) | Perfect positive linear relationship |
|      \(+0.8\) | Strong positive relationship         |
|      \(+0.5\) | Moderate positive relationship       |
|         \(0\) | No linear relationship               |
|      \(-0.5\) | Moderate negative relationship       |
|      \(-0.8\) | Strong negative relationship         |
|        \(-1\) | Perfect negative linear relationship |

### Positive correlation

$$
r>0
$$

When one variable increases, the other tends to increase.

```text
X ↑
 ↓
Y ↑
```

Example:

**Hours studied ↑ → Exam score tends to ↑**

---

### Negative correlation

$$
r<0
$$

When one variable increases, the other tends to decrease.

```text
X ↑
 ↓
Y ↓
```

Example:

**Price ↑ → Quantity demanded tends to ↓**

---

### Zero correlation

$$
r\approx0
$$

There is no clear **linear** relationship.

---

# 3. Why is Pearson Correlation Useful?

Suppose you have data about:

* Advertising spend
* Sales

You might ask:

> "Do higher advertising expenditures tend to be associated with higher sales?"

Pearson correlation gives you a quick numerical summary of the **linear association**.

For example:

$$
r=0.85
$$

This indicates a **strong positive linear association**.

But it does **not** tell you that advertising caused the increase in sales.

---

# 4. Pearson Correlation Formula

The sample Pearson correlation coefficient is:

$$
\boxed{
r=
\frac{
\sum_{i=1}^{n}(X_i-\bar X)(Y_i-\bar Y)
}{
\sqrt{
\sum_{i=1}^{n}(X_i-\bar X)^2
\sum_{i=1}^{n}(Y_i-\bar Y)^2
}
}
}
$$

Don't worry about memorizing the entire formula initially.

The intuition is more important:

$$
\boxed{
r=
\frac{\text{Covariance}}
{\text{Standard deviation of X}\times\text{Standard deviation of Y}}
}
$$

So Pearson correlation is essentially **standardized covariance**.

---

# 5. Covariance vs Pearson Correlation

You just learned covariance, so this connection is important.

### Covariance

$$
\operatorname{Cov}(X,Y)
$$

tells us whether variables move together and in which direction.

But covariance depends on the units.

### Pearson correlation

$$
r=
\frac{\operatorname{Cov}(X,Y)}
{\sigma_X\sigma_Y}
$$

standardizes covariance.

Therefore:

$$
\boxed{-1\le r\le1}
$$

and correlation is **unitless**.

### Example

If height is measured in:

* meters → correlation stays the same
* centimeters → correlation stays the same

That's a major advantage of correlation.

---

# 6. Simple Example

Suppose:

| Student | Study Hours | Score |
| ------- | ----------: | ----: |
| A       |           1 |    50 |
| B       |           2 |    55 |
| C       |           3 |    65 |
| D       |           4 |    70 |
| E       |           5 |    80 |

As study hours increase, scores generally increase.

So we would expect:

$$
\boxed{r>0}
$$

and probably a fairly strong positive correlation.

Conceptually:

```text
Score
  ↑
80|             ●
70|          ●
65|       ●
55|    ●
50| ●
  +----------------→ Study Hours
    1   2   3   4   5
```

The more closely the points follow an upward-sloping straight-line pattern, the closer \(r\) is to \(+1\).

---

# 7. What Does "Strength" Mean?

Consider two datasets.

### Dataset A

```text
      ●
    ●
   ●
 ●
●
```

The points are close to a straight line.

$$
r\approx+1
$$

### Dataset B

```text
   ●       ●
      ●
 ●       ●
      ●
```

There is a much weaker linear pattern.

$$
r\approx0
$$

So:

> **The closer \(|r|\) is to 1, the stronger the linear relationship.**

The closer \(r\) is to 0, the weaker the linear relationship.

---

# 8. Important: Correlation Only Measures Linear Relationships

This is one of the **most important concepts**.

Pearson correlation measures **linear** association.

Suppose:

$$
Y=X^2
$$

There is a very clear relationship between \(X\) and \(Y\), but it is **nonlinear**.

Pearson's \(r\) may be close to zero depending on the distribution of \(X\).

Therefore:

$$
\boxed{r\approx0\not\Rightarrow\text{No relationship}}
$$

It means:

> There may be no **linear** relationship.

---

# 9. Correlation Does NOT Mean Causation

Suppose we find:

$$
r=0.90
$$

between ice cream sales and swimming activity.

Does eating ice cream cause people to swim?

Not necessarily.

A third variable could explain both:

```text
        Temperature
        ↙         ↘
Ice cream       Swimming
  sales ↑       activity ↑
```

Hot weather may cause both ice cream sales and swimming activity to increase.

Therefore:

$$
\boxed{\text{Correlation}\neq\text{Causation}}
$$

---

# 10. Pearson Correlation vs Covariance

| Feature                               | Covariance | Pearson Correlation |
| ------------------------------------- | ---------- | ------------------- |
| Measures co-movement                  | ✅          | ✅                   |
| Shows direction                       | ✅          | ✅                   |
| Shows standardized strength           | ❌          | ✅                   |
| Range                                 | Unbounded  | \([-1,+1]\)         |
| Depends on units                      | ✅          | ❌                   |
| Easy to compare across variable pairs | ❌          | ✅                   |
| Unitless                              | ❌          | ✅                   |

### Mental model

> **Covariance = raw co-movement**

> **Correlation = standardized co-movement**

---

# 11. Pearson Correlation vs \(R^2\)

Another important Data Science connection.

If you have a simple linear regression with one predictor, then:

$$
\boxed{R^2=r^2}
$$

For example:

$$
r=0.8
$$

Then:

$$
R^2=0.8^2=0.64
$$

So approximately **64% of the variation in the response is explained by the linear model** in that simple-regression setting.

⚠️ Be careful: this interpretation is about the **linear regression model** and does not mean 64% of one variable "causes" the other.

---

# 12. What Does \(r=0.8\) Actually Mean?

Suppose:

$$
r=0.8
$$

This means:

> There is a strong positive **linear association** between the two variables.

It does **not** mean:

* \(X\) causes \(Y\)
* \(Y\) causes \(X\)
* \(Y\) increases by 80% when \(X\) increases
* 80% of observations follow the relationship
* There is an 80% probability that the relationship is real

The number \(0.8\) specifically describes the **strength and direction of linear association**.

---

# 13. Pearson Correlation and Outliers

Pearson correlation can be **strongly affected by outliers**.

Imagine most observations look like:

```text
●
 ●
  ●
   ●
```

Then one extreme observation appears far away.

That single point can significantly change \(r\).

Therefore, before interpreting Pearson correlation:

> **Always inspect the data, ideally with a scatter plot.**

---

# 14. Pearson Correlation and Statistical Significance

There are two different questions:

### Question 1: How strong is the relationship?

Use:

$$
\boxed{r}
$$

### Question 2: Is there evidence that the population correlation differs from zero?

You can perform a hypothesis test.

For example:

$$
H_0:\rho=0
$$

$$
H_1:\rho\ne0
$$

where \(\rho\) is the **population correlation**.

A p-value can then be used to assess evidence against \(H_0\).

So don't confuse:

$$
\boxed{\text{Correlation coefficient}}
$$

with:

$$
\boxed{\text{Statistical significance}}
$$

A tiny correlation can be statistically significant with a huge sample, while a meaningful correlation may fail to reach significance with a very small sample.

---

# 15. Pearson vs Spearman Correlation

This is very useful in Data Science.

| Pearson                                     | Spearman                                         |
| ------------------------------------------- | ------------------------------------------------ |
| Measures linear relationship                | Measures monotonic relationship                  |
| Uses actual values                          | Uses ranks                                       |
| Sensitive to outliers                       | Often more robust to outliers                    |
| Best for approximately linear relationships | Useful for monotonic but nonlinear relationships |
| Usually assumes numerical/continuous data   | Can work well with ordinal/ranked data           |

### Example

If:

$$
X\uparrow \Rightarrow Y\uparrow
$$

but the relationship is curved rather than straight, **Spearman correlation** may capture the association better than Pearson.

---

# 16. When Should You Use Pearson Correlation?

Pearson correlation is useful when:

* Both variables are numerical.
* You are interested in a **linear relationship**.
* The data are reasonably suitable for Pearson's assumptions.
* You want a standardized measure between \(-1\) and \(+1\).

Common applications:

### Data Science

Checking relationships between numerical features.

### Exploratory Data Analysis

Understanding how variables relate.

### Finance

Studying relationships between asset returns.

### Business

Examining relationships between advertising and sales.

### Research

Studying associations between quantitative measurements.

---

# 17. A Practical Data Science Example

Suppose you have:

```text
Feature 1 → Advertising Spend
Feature 2 → Sales
Feature 3 → Website Traffic
Feature 4 → Customer Age
```

You calculate the correlation matrix:

```text
                 Sales   Traffic   Age
Sales             1.00     0.82    0.05
Traffic           0.82     1.00    0.02
Age               0.05     0.02    1.00
```

Interpretation:

* Sales ↔ Traffic: strong positive linear association
* Sales ↔ Age: very weak linear association
* Traffic ↔ Age: very weak linear association

This can help during **exploratory data analysis** and feature investigation.

But correlation alone should not be used to conclude causality.

---

# 18. Important Limitations

Pearson correlation:

1. Measures **linear** association.
2. Can be affected by **outliers**.
3. Does not establish **causation**.
4. Can be misleading when important subgroups are mixed together.
5. A statistically significant correlation may still be practically unimportant.
6. A correlation near zero does not rule out a nonlinear relationship.

---

# 19. Interview-Ready Answer

> **Pearson's correlation coefficient measures the strength and direction of the linear relationship between two numerical variables. It ranges from -1 to +1, where +1 represents a perfect positive linear relationship, -1 represents a perfect negative linear relationship, and 0 indicates no linear relationship. It is essentially standardized covariance, making it unitless and easier to compare across variables. However, correlation does not imply causation and Pearson correlation may be sensitive to outliers and nonlinear relationships.**

---

# 20. Mental Model

Remember:

```text
             PEARSON CORRELATION
                     │
             ┌───────┴───────┐
             ↓               ↓
        Direction          Strength
             │               │
      Positive / Negative   0 → 1
             │
             └───────┬───────┘
                     ↓
              Linear relationship
```

### The most important interpretation

$$
\boxed{
r>0\Rightarrow\text{positive linear association}
}
$$

$$
\boxed{
r<0\Rightarrow\text{negative linear association}
}
$$

$$
\boxed{
|r|\approx1\Rightarrow\text{strong linear association}
}
$$

$$
\boxed{
r\approx0\Rightarrow\text{little/no linear association}
}
$$

### One-line takeaway

> **Pearson correlation tells us how strongly and in what direction two numerical variables are linearly associated, on a standardized scale from -1 to +1.**
