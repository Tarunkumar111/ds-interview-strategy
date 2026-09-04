# StatQuickie: Which t-test to Use?

There are several types of t-tests, and the easiest way to choose the right one is to ask:

> **How many groups or conditions am I comparing, and are the observations independent or paired?**

---

# 1. The Three Main t-tests

There are three common situations:

```text
                 Which t-test?
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
     One group?              Two groups?
          │                       │
          ↓                 ┌─────┴─────┐
   One-sample t-test        ↓           ↓
                         Independent   Paired
                           groups       data
                             ↓           ↓
                    Independent t-test  Paired t-test
```

---

# 2. One-Sample t-test

Use a **one-sample t-test** when you have:

> **One group of observations and want to compare its mean with a known or hypothesized value.**

### Example

Suppose the company claims:

$$
\mu=50
$$

You collect data from 30 customers.

Their average spending is:

$$
\bar{x}=54
$$

You want to ask:

> Is the population mean different from 50?

Hypotheses:

$$
H_0:\mu=50
$$

$$
H_1:\mu\ne50
$$

Use:

> **One-sample t-test**

---

# 3. Independent Two-Sample t-test

Use an **independent two-sample t-test** when you have:

> **Two independent groups and want to compare their means.**

### Example

You want to compare salaries between:

```text
Group A → Employees using Tool A
Group B → Employees using Tool B
```

Different employees are in each group.

```text
Tool A
Person 1
Person 2
Person 3
...

Tool B
Person 4
Person 5
Person 6
...
```

The observations are independent between groups.

Use:

> **Independent two-sample t-test**

---

# 4. Paired t-test

Use a **paired t-test** when observations naturally come in pairs.

The most common example is:

> **Before vs after measurements on the same subjects.**

Example:

| Person | Before | After |
| ------ | -----: | ----: |
| 1      |     80 |    75 |
| 2      |     85 |    79 |
| 3      |     90 |    84 |
| 4      |     78 |    76 |

Each person's measurements are paired.

We don't treat:

```text
Before → independent group
After  → independent group
```

Instead, we calculate the difference for each person:

$$
D_i=After_i-Before_i
$$

Then perform a **one-sample t-test on the differences**:

$$
H_0:\mu_D=0
$$

That's the key mathematical idea behind the paired t-test.

---

# 5. The Three Tests Side by Side

| Situation                         | Test                          |
| --------------------------------- | ----------------------------- |
| One group vs known value          | One-sample t-test             |
| Two independent groups            | Independent two-sample t-test |
| Two paired/dependent measurements | Paired t-test                 |

---

# 6. The Most Important Question: Are the Groups Independent?

This is often the easiest way to decide.

### Independent

Different people/items are in each group.

```text
Group A          Group B
Person 1         Person 10
Person 2         Person 11
Person 3         Person 12
```

Use:

> **Independent two-sample t-test**

---

### Paired

The same person/item is measured twice.

```text
Person 1 → Before → After
Person 2 → Before → After
Person 3 → Before → After
```

Use:

> **Paired t-test**

---

# 7. Example: A/B Test

Suppose an e-commerce company tests two website designs.

```text
Users randomly assigned:

Group A → Old website
Group B → New website
```

Different users are in each group.

If the outcome is numerical, such as revenue per user:

> **Independent two-sample t-test**

You might test:

$$
H_0:\mu_A=\mu_B
$$

against:

$$
H_1:\mu_A\ne\mu_B
$$

---

# 8. Example: Before and After

Suppose you measure employee productivity before and after training.

```text
Employee 1 → Before / After
Employee 2 → Before / After
Employee 3 → Before / After
```

Because the same employees are measured twice:

> **Paired t-test**

Calculate:

$$
D_i=After_i-Before_i
$$

Then test:

$$
H_0:\mu_D=0
$$

---

# 9. Example: One-Sample

Suppose a manufacturer claims:

> Average battery life is 10 hours.

You test 25 batteries.

Your question is:

> Is the true mean battery life different from 10 hours?

Only one sample is involved.

Use:

> **One-sample t-test**

---

# 10. What About Equal Variances?

For the independent two-sample case, there are two common versions.

### Student's two-sample t-test

Assumes equal population variances.

### Welch's t-test

Does **not** assume equal population variances.

In practice, **Welch's t-test is often a good default for comparing two independent means**, particularly when group variances or sample sizes may differ.

The test statistic is:

$$
t=
\frac{\bar{x}_1-\bar{x}_2}
{\sqrt{\frac{s_1^2}{n_1}+\frac{s_2^2}{n_2}}}
$$

The degrees of freedom are estimated using the **Welch–Satterthwaite approximation**.

---

# 11. Student vs Welch

| Feature                   | Student's t-test                      | Welch's t-test    |
| ------------------------- | ------------------------------------- | ----------------- |
| Two independent groups    | Yes                                   | Yes               |
| Equal variance assumption | Yes                                   | No                |
| Unequal variances         | Not appropriate without justification | Designed for this |
| Common practical choice   | Less often preferred as default       | Often preferred   |

### Important

You don't necessarily need to perform a preliminary "equal variance test" and then mechanically choose between Student and Welch. Welch's test is generally robust and is often the safer default.

---

# 12. One-Tailed vs Two-Tailed

After choosing the type of t-test, you also need to determine the **direction of the hypothesis**.

### Two-tailed

You want to know whether the means are different:

$$
H_1:\mu_1\ne\mu_2
$$

### Right-tailed

You specifically expect one mean to be larger:

$$
H_1:\mu_1>\mu_2
$$

### Left-tailed

$$
H_1:\mu_1<\mu_2
$$

The direction should generally be specified **before looking at the results**.

---

# 13. Decision Tree

Use this simple decision tree:

```text
                 What are you comparing?
                         │
          ┌──────────────┴──────────────┐
          ↓                             ↓
       One group                    Two groups
          │                             │
          ↓                    Are observations paired?
   Compare mean to                    │
   a known value             ┌────────┴────────┐
                             ↓                 ↓
                            Yes                No
                             ↓                 ↓
                        Paired t-test    Independent
                                         two-sample t-test
```

---

# 14. Python: One-Sample t-test

Using SciPy:

```python
from scipy.stats import ttest_1samp

data = [52, 48, 51, 55, 49, 53, 50]

result = ttest_1samp(
    data,
    popmean=50
)

print(result)
```

This tests:

$$
H_0:\mu=50
$$

---

# 15. Python: Independent t-test

Suppose:

```python
group_a = [70, 72, 68, 71, 69]
group_b = [78, 80, 76, 81, 79]
```

Use Welch's test:

```python
from scipy.stats import ttest_ind

result = ttest_ind(
    group_a,
    group_b,
    equal_var=False
)

print(result)
```

`equal_var=False` specifies Welch's t-test.

---

# 16. Python: Paired t-test

Suppose:

```python
before = [80, 85, 90, 78, 88]
after  = [75, 81, 84, 76, 83]
```

Use:

```python
from scipy.stats import ttest_rel

result = ttest_rel(
    before,
    after
)

print(result)
```

This tests whether the **mean paired difference** is zero.

---

# 17. What Does the t-test Actually Test?

The core idea is always:

$$
t=
\frac{\text{Observed difference from null}}
{\text{Standard error}}
$$

For a one-sample test:

$$
t=
\frac{\bar{x}-\mu_0}
{s/\sqrt n}
$$

For a two-independent-sample test:

$$
t=
\frac{\bar{x}_1-\bar{x}_2}
{SE(\bar{x}_1-\bar{x}_2)}
$$

For a paired test:

$$
t=
\frac{\bar{D}-0}
{s_D/\sqrt n}
$$

Notice the common structure.

---

# 18. The Beautiful Connection

A paired t-test can be reduced to a one-sample t-test.

Suppose:

$$
D_i=After_i-Before_i
$$

Then:

$$
H_0:\mu_D=0
$$

And we perform a one-sample t-test on:

$$
D_1,D_2,\ldots,D_n
$$

So:

```text
Paired data
   ↓
Calculate differences
   ↓
D = After − Before
   ↓
One-sample t-test
   ↓
Paired t-test
```

This is a very useful mental model.

---

# 19. t-tests and Linear Models

This connects directly to your previous topic.

A two-group t-test can be represented as a linear model:

$$
Y=\beta_0+\beta_1Group+\epsilon
$$

where:

```text
Control   = 0
Treatment = 1
```

Then:

$$
\beta_1
=
Mean(Treatment)-Mean(Control)
$$

and testing:

$$
H_0:\beta_1=0
$$

is equivalent to the corresponding two-group t-test under the standard setup.

So:

```text
Two-group t-test
       ↓
Categorical predictor
       ↓
Linear model
       ↓
Coefficient t-test
```

---

# 20. When Should You NOT Use a t-test?

A t-test isn't automatically appropriate whenever you have two groups.

Consider other methods when:

### More than two groups

Use ANOVA or an appropriate regression/modeling approach.

```text
A vs B vs C
     ↓
ANOVA
```

### Binary outcome

For example:

```text
Purchased / Didn't purchase
```

A t-test on raw 0/1 outcomes can be mathematically related to a two-group comparison, but proportion-specific methods or logistic regression are often more natural depending on the question/design.

### Strong dependence or clustering

Repeated measurements, matched designs, classrooms, hospitals, etc. may require models that account for the dependence structure.

### Very small or unusual samples

You may need to consider the data distribution, robustness, transformations, or nonparametric methods.

---

# 21. t-test vs Mann–Whitney U

A common misconception is:

> "If the data aren't normal, always use Mann–Whitney."

Not necessarily.

The t-test can be reasonably robust to moderate departures from normality, especially with adequate sample sizes and well-behaved data.

Mann–Whitney tests a different quantity and has its own assumptions.

So don't mechanically switch tests just because a histogram isn't perfectly bell-shaped.

---

# 22. Important Assumptions

Depending on the specific t-test, assumptions include:

### One-sample / paired

The observations being analyzed should be appropriately independent, and the distribution of the observations/differences should be reasonably suitable for the t procedure, especially for small samples.

### Independent two-sample

The two groups should be independent, and Welch's test avoids the equal-variance assumption.

Extreme outliers can still cause problems.

---

# 23. The Quick Cheat Sheet

| Question                        | Answer | Test                                 |
| ------------------------------- | ------ | ------------------------------------ |
| One group vs known value?       | Yes    | One-sample t-test                    |
| Two groups?                     | Yes    | Continue                             |
| Same subjects measured twice?   | Yes    | Paired t-test                        |
| Matched pairs?                  | Yes    | Paired t-test                        |
| Different independent subjects? | Yes    | Independent two-sample t-test        |
| Unequal variances likely?       | Yes    | Welch's t-test                       |
| 3+ groups?                      | Yes    | ANOVA / regression                   |
| Binary outcome?                 | Yes    | Consider proportion/logistic methods |

---

# 🧠 Mental Model

Don't memorize three test names separately.

Ask these questions:

```text
1. How many groups?
       ↓
2. One or two?
       ↓
3. If two: Are they paired?
       ↓
4. If independent: Are equal variances
   a reasonable assumption?
       ↓
5. Choose one-tailed or two-tailed
   based on the hypothesis
```

Then:

```text
One group
   → One-sample t-test

Two paired groups
   → Paired t-test

Two independent groups
   → Two-sample t-test
      → Welch is often a good default
```

---

# 🎯 Interview-Ready Answer

> **I choose a t-test based mainly on the number of groups and whether observations are paired. A one-sample t-test compares one sample mean with a hypothesized value. An independent two-sample t-test compares means from two independent groups, with Welch's version commonly preferred when equal variances cannot be assumed. A paired t-test is used when measurements are naturally paired, such as before-and-after measurements on the same subjects; mathematically, it is equivalent to a one-sample t-test on the within-pair differences.**

---

## 🔑 One-Line Takeaway

> **One group → one-sample t-test; two paired groups → paired t-test; two independent groups → independent two-sample t-test, often using Welch's version when variances may differ.**
