# Why Dividing By N Underestimates the Variance

This is one of the most important ideas behind **sample variance** and the famous **\(n-1\) correction**.

The short answer is:

> **When we estimate variance from a sample, we use the sample mean instead of the true population mean. Because the sample mean is estimated from the same data, the deviations tend to be slightly smaller than they would be around the true population mean. Dividing by \(n\) therefore systematically underestimates the population variance.**

The solution is **Bessel's correction**:

$$
\boxed{s^2=\frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}}
$$

Let's understand why.

---

# 1. Population Variance vs Sample Variance

If we have the **entire population**, we know the true population mean:

$$
\mu
$$

So population variance is:

$$
\boxed{
\sigma^2=\frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)^2
}
$$

Here dividing by \(N\) is correct.

---

But suppose we only have a **sample**.

We don't know the population mean \(\mu\).

So we estimate it using the sample mean:

$$
\bar{x}
$$

Then we calculate:

$$
\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

The problem is that this tends to be **too small** as an estimator of the population variance.

So we use:

$$
\boxed{
s^2=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2
}
$$

---

# 2. The Key Reason: We Estimated the Mean

Imagine you have these observations:

$$
2,\ 4,\ 6,\ 8,\ 10
$$

The sample mean is:

$$
\bar{x}=6
$$

The deviations are:

$$
-4,-2,0,2,4
$$

Notice something:

> The sample mean is calculated specifically to be the point that minimizes the sum of squared deviations.

That is:

$$
\boxed{
\bar{x}=\arg\min_c\sum(x_i-c)^2
}
$$

In simpler words:

> **The sample mean is the center that makes the squared deviations as small as possible.**

So when we calculate variance around \(\bar{x}\), we're using a center that was **chosen from the data to minimize those deviations**.

That creates a downward bias.

---

# 3. Visual Intuition

Imagine the true population mean is here:

```text
Population
────────────────────────────────
              μ
              │
        •  •  •  •  •
```

But from our sample, we estimate the mean:

```text
Sample
────────────────────────────────
            μ      x̄
            │      │
       •  • • • •  •
```

The sample mean \(\bar{x}\) tends to move toward the observations in that particular sample.

Therefore:

$$
\text{Distance from observations to }\bar{x}
$$

tends to be smaller than:

$$
\text{Distance from observations to }\mu
$$

on average.

---

# 4. A Simple Extreme Example

Suppose our sample contains only:

$$
5,\ 5
$$

The sample mean is:

$$
\bar{x}=5
$$

Therefore:

$$
(5-5)^2+(5-5)^2=0
$$

So dividing by \(n=2\) gives:

$$
0/2=0
$$

But imagine these two observations came from a population with genuine variability.

The sample happened to contain two identical values.

Our sample variance of zero would underestimate the population variance.

The problem becomes even more obvious with:

$$
n=1
$$

If you have one observation:

$$
x_1=5
$$

then:

$$
\bar{x}=5
$$

and:

$$
(x_1-\bar{x})^2=0
$$

Dividing by \(n=1\):

$$
0/1=0
$$

But one observation clearly doesn't give us enough information to conclude that the population variance is zero.

That's why the unbiased sample variance formula has:

$$
n-1
$$

in the denominator.

---

# 5. The Mathematical Reason

Here's the beautiful result:

$$
\boxed{
E\left[
\frac{1}{n}\sum_{i=1}^{n}(X_i-\bar X)^2
\right]
=
\frac{n-1}{n}\sigma^2
}
$$

Therefore, the estimator using \(n\):

$$
s_n^2=
\frac{1}{n}\sum(X_i-\bar X)^2
$$

has expected value:

$$
E[s_n^2]
=
\frac{n-1}{n}\sigma^2
$$

Since:

$$
\frac{n-1}{n}<1
$$

we have:

$$
E[s_n^2]<\sigma^2
$$

So it **systematically underestimates** the population variance.

---

# 6. Why Does \(n-1\) Fix It?

The sample variance is:

$$
s^2=
\frac{1}{n-1}\sum(X_i-\bar X)^2
$$

Now consider its expectation:

$$
E[s^2]
=
E\left[
\frac{1}{n-1}
\sum(X_i-\bar X)^2
\right]
$$

The expected numerator is:

$$
(n-1)\sigma^2
$$

Therefore:

$$
E[s^2]
=
\frac{(n-1)\sigma^2}{n-1}
$$

$$
\boxed{E[s^2]=\sigma^2}
$$

So \(s^2\) is an **unbiased estimator** of the population variance under the usual random-sample assumptions.

---

# 7. Where Did That "One" Go?

This is the famous **degrees of freedom** idea.

Suppose you have \(n\) observations:

$$
x_1,x_2,\ldots,x_n
$$

Once you've calculated the sample mean \(\bar{x}\), the deviations must satisfy:

$$
\sum_{i=1}^{n}(x_i-\bar{x})=0
$$

That means if you know \(n-1\) deviations, the final deviation is automatically determined.

For example, suppose:

$$
x_1-\bar{x}=2
$$

$$
x_2-\bar{x}=-3
$$

$$
x_3-\bar{x}=4
$$

Then the final deviation must be:

$$
-2-(-3)-4=-3
$$

so that all deviations add to zero.

Therefore, only:

$$
\boxed{n-1}
$$

deviations are freely variable.

---

# 8. That's What "Degrees of Freedom" Means

Degrees of freedom are, roughly:

> **How many independent pieces of information are available after accounting for estimated parameters/constraints?**

For sample variance:

* Start with \(n\) observations
* Estimate one parameter: the mean
* Lose one degree of freedom

Therefore:

$$
\boxed{df=n-1}
$$

And that's why:

$$
\boxed{s^2=\frac{SS}{df}=\frac{SS}{n-1}}
$$

---

# 9. A Concrete Example

Suppose:

$$
X=[10,20,30]
$$

Sample mean:

$$
\bar{x}=20
$$

Deviations:

$$
-10,\ 0,\ +10
$$

Squared deviations:

$$
100,\ 0,\ 100
$$

Sum:

$$
200
$$

### Divide by \(n=3\)

$$
\frac{200}{3}=66.67
$$

### Divide by \(n-1=2\)

$$
\frac{200}{2}=100
$$

So:

$$
\boxed{\text{Variance using }n=66.67}
$$

while:

$$
\boxed{\text{Sample variance using }n-1=100}
$$

The \(n-1\) version is deliberately larger because the \(n\) version is biased downward.

---

# 10. Why Is the Difference Small for Large Samples?

Look at:

$$
\frac{n}{n-1}
$$

For \(n=5\):

$$
\frac{5}{4}=1.25
$$

That's a 25% correction.

For \(n=10\):

$$
\frac{10}{9}\approx1.111
$$

About 11%.

For \(n=100\):

$$
\frac{100}{99}\approx1.010
$$

Only about 1%.

So:

```text
Small sample
    ↓
Large correction

Large sample
    ↓
Small correction
```

This is why the distinction becomes less important as \(n\) gets very large.

---

# 11. Important: It's Not Because "N Is Always Wrong"

This is a crucial distinction.

### If you have the entire population:

Use:

$$
\boxed{
\sigma^2=\frac{\sum(x_i-\mu)^2}{N}
}
$$

### If you're estimating population variance from a sample:

Use:

$$
\boxed{
s^2=\frac{\sum(x_i-\bar{x})^2}{n-1}
}
$$

So:

> **\(N\) is not inherently wrong. The denominator depends on whether you're describing the entire population or estimating its variance from a sample.**

---

# 12. Connection to Standard Deviation

Variance:

$$
s^2=
\frac{\sum(x_i-\bar{x})^2}{n-1}
$$

Standard deviation is simply the square root:

$$
\boxed{
s=\sqrt{
\frac{\sum(x_i-\bar{x})^2}{n-1}
}
}
$$

So the same \(n-1\) correction appears in the sample standard deviation.

---

# 13. Connection to What You've Already Learned

This connects directly to **population vs estimated parameters**.

```text
Population
   │
   ├── True mean μ
   │
   └── True variance σ²
           ↓
        Unknown
           │
           ▼
         Sample
           │
           ├── Sample mean x̄
           │
           └── Sample variance s²
                         ↓
                   Estimate of σ²
```

Because we don't know \(\mu\), we estimate it with \(\bar{x}\).

That costs us **one degree of freedom**.

Therefore:

$$
n\rightarrow n-1
$$

---

# 14. Connection to Standard Error

Remember:

$$
SE(\bar{x})=\frac{s}{\sqrt n}
$$

The \(s\) here is usually calculated using:

$$
n-1
$$

because we're estimating the population standard deviation from the sample.

So:

```text
Sample data
     ↓
Sample mean x̄
     ↓
Sample variance s²
     ↓
Sample SD s
     ↓
Standard Error
     ↓
Confidence Interval / Hypothesis Test
```

This small-looking \(n-1\) correction ultimately affects many statistical procedures.

---

# 15. The Deepest Intuition

Here's the idea worth remembering:

> **The sample mean "uses up" one degree of freedom and makes the observed deviations artificially small.**

Therefore:

```text
Estimate mean from sample
          ↓
Mean moves toward sample observations
          ↓
Deviations become slightly smaller
          ↓
Squared deviations become slightly smaller
          ↓
Dividing by n underestimates variance
          ↓
Use n − 1 to correct the bias
```

---

# Interview-Ready Answer

> **We divide by \(n-1\) rather than \(n\) when estimating population variance from a sample because the sample mean is estimated from the same data. This makes the deviations around the sample mean systematically smaller than deviations around the true population mean. As a result, dividing by \(n\) produces a downward-biased estimator of population variance. Using \(n-1\), known as Bessel's correction, gives an unbiased estimator under the usual random-sampling assumptions. The subtraction of 1 reflects the one degree of freedom used to estimate the sample mean.**

## 🧠 Mental Model

> **We lose one degree of freedom because we estimated the mean.**

$$
\boxed{
\text{Sample variance}
=
\frac{\text{Sum of squared deviations}}{n-1}
}
$$

### One-line takeaway

$$
\boxed{
\text{Divide by }n\text{ when describing a known full population;}
\quad
\text{divide by }n-1\text{ when estimating population variance from a sample.}
}
$$
