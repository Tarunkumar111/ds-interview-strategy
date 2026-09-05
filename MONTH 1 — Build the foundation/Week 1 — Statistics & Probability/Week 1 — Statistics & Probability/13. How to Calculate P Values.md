# How to Calculate P-values

A **p-value** is calculated from a **test statistic** and tells us how extreme our observed result is under the assumption that the **null hypothesis (H₀) is true**.

The general process is:

```text
Data
  ↓
Define H₀ and H₁
  ↓
Choose a statistical test
  ↓
Calculate test statistic
  ↓
Find probability beyond that statistic
  ↓
p-value
```

---

## 1. Simple Example — Z-test

Suppose a company claims:

> **The average delivery time is 30 minutes.**

We want to test whether the actual average is different.

### Hypotheses

```text
H₀: μ = 30 minutes
H₁: μ ≠ 30 minutes
```

Suppose we collect a sample:

```text
Sample mean = 32 minutes
Population standard deviation = 10 minutes
Sample size = 100
```

---

## 2. Calculate the Test Statistic

For a one-sample Z-test:

$$
z = \frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}
$$

Where:

* \(\bar{x}\) = sample mean
* \(\mu_0\) = mean assumed by H₀
* \(\sigma\) = population standard deviation
* \(n\) = sample size

Plug in our values:

$$
z = \frac{32-30}{10/\sqrt{100}}
$$

$$
z = \frac{2}{1}
$$

$$
\boxed{z=2}
$$

So our observed result is **2 standard errors above the mean assumed by H₀**.

---

## 3. Convert the Test Statistic into a P-value

Now we need to ask:

> If H₀ is true, how likely is it to observe a result this extreme or more extreme?

Because our alternative hypothesis is:

$$
H_1:\mu\neq30
$$

this is a **two-tailed test**.

For \(z=2\):

```text
             Normal Distribution

                 /\
               /    \
             /        \
────────────/──────────\────────────
          -2    0       +2
           ←───┘ └────→
             Tail areas
```

The probability beyond \(z=2\) on one side is approximately:

$$
0.0228
$$

Because it's a two-tailed test:

$$
p = 2(0.0228)
$$

$$
\boxed{p\approx0.0456}
$$

---

# 4. Compare with α

Suppose we chose:

$$
\alpha=0.05
$$

We have:

$$
p=0.0456
$$

Therefore:

$$
0.0456 < 0.05
$$

So:

> **Reject H₀.**

There is statistically significant evidence that the average delivery time differs from 30 minutes.

---

# 5. The Important Part: The Test Determines How You Calculate the P-value

The calculation depends on the statistical test and the alternative hypothesis.

### Right-tailed test

If:

$$
H_1:\mu>\mu_0
$$

then:

$$
p=P(Z\geq z)
$$

You look at the **right tail**.

---

### Left-tailed test

If:

$$
H_1:\mu<\mu_0
$$

then:

$$
p=P(Z\leq z)
$$

You look at the **left tail**.

---

### Two-tailed test

If:

$$
H_1:\mu\neq\mu_0
$$

then you consider extreme results in **both directions**.

For a symmetric Z distribution:

$$
p=2P(Z\geq|z|)
$$

---

# 6. Different Tests Use Different Distributions

You don't always calculate a p-value using a Z-score.

The process is:

> **Calculate the appropriate test statistic → use its sampling distribution → calculate the relevant tail probability.**

For example:

| Test                | Test statistic / distribution      |
| ------------------- | ---------------------------------- |
| Z-test              | Z / Standard Normal                |
| t-test              | t-distribution                     |
| Chi-square test     | Chi-square distribution            |
| ANOVA               | F-distribution                     |
| Fisher's Exact Test | Exact/hypergeometric probabilities |

So the **p-value calculation depends on the test you're performing**.

---

# 7. Example with a t-test

Suppose you don't know the population standard deviation.

You have:

```text
Sample mean = 32
Hypothesized mean = 30
Sample SD = 10
Sample size = 25
```

You would typically use a **t-test**.

Calculate:

$$
t=\frac{\bar{x}-\mu_0}{s/\sqrt n}
$$

$$
t=\frac{32-30}{10/\sqrt{25}}
$$

$$
t=\frac{2}{2}
$$

$$
\boxed{t=1}
$$

Now we use the **t-distribution with \(n-1=24\) degrees of freedom** to calculate the tail probability.

That's the p-value.

---

# 8. Using Python

In real Data Science work, you normally **don't calculate the p-value manually**.

Libraries such as SciPy can calculate it for you.

For example, for a one-sample t-test:

```python
from scipy import stats

sample = [28, 30, 31, 32, 29, 35, 30, 33]

result = stats.ttest_1samp(sample, 30)

print(result.statistic)
print(result.pvalue)
```

The important thing is not memorizing the library syntax.

Understand the logic:

```text
Sample
  ↓
Choose test
  ↓
Calculate test statistic
  ↓
Use appropriate probability distribution
  ↓
Calculate p-value
```

---

# 9. Very Important: P-value Is Not Always "Area to the Right"

This is a common beginner mistake.

The p-value depends on the **alternative hypothesis**.

```text
H₁: μ > μ₀
→ Right-tail

H₁: μ < μ₀
→ Left-tail

H₁: μ ≠ μ₀
→ Both tails
```

So you should **always look at H₁ before calculating the p-value**.

---

# 10. Fisher's Exact Test Example

Since you just learned Fisher's Exact Test, here's how it connects.

Suppose you have:

|         | Success | Failure |
| ------- | ------: | ------: |
| Group A |       1 |       9 |
| Group B |       5 |       5 |

Fisher's Exact Test doesn't calculate a Z or t statistic.

Instead, it uses the **hypergeometric distribution** to calculate the probability of the observed table and tables that are at least as extreme.

The resulting probability is the **p-value**.

So:

```text
Z-test
→ Z statistic → Normal distribution → p-value

t-test
→ t statistic → t-distribution → p-value

Fisher's Exact
→ Hypergeometric probabilities → p-value
```

---

# 11. The Big Picture

The most important thing to understand is:

> **A p-value is not something you calculate directly from the raw data using one universal formula.**

Instead:

```text
             Raw Data
                ↓
        Define H₀ and H₁
                ↓
         Choose a test
                ↓
       Calculate statistic
                ↓
   Identify sampling distribution
                ↓
       Calculate tail probability
                ↓
             P-value
                ↓
         Compare with α
                ↓
      Reject / Fail to reject H₀
```

---

# Interview-Ready Answer

If an interviewer asks:

**"How do you calculate a p-value?"**

You can answer:

> **First, we define the null and alternative hypotheses and choose an appropriate statistical test. We calculate the test statistic from the sample data, determine its sampling distribution under the null hypothesis, and then calculate the probability of obtaining a result at least as extreme as the observed statistic. That probability is the p-value. Finally, we compare it with the chosen significance level to make a decision about the null hypothesis.**

### Remember this:

> **Test statistic → Sampling distribution → Tail probability → P-value**

That's the core idea.
