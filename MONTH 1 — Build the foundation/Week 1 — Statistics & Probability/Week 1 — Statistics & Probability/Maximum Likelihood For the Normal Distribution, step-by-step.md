# Maximum Likelihood for the Normal Distribution, Step-by-Step!!!

The **Normal distribution** is one of the most important places to understand Maximum Likelihood Estimation (MLE).

We will start with observed data and derive, step by step, why the MLEs are:

$$
\boxed{\hat{\mu}=\bar{x}}
$$

and

$$
\boxed{
\hat{\sigma}^2
=
\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2
}
$$

Notice something surprising:

> **The MLE for variance divides by \(n\), not \(n-1\).**

We'll see exactly why.

---

# 1. Start With the Normal Distribution

The Normal probability density function is:

$$
f(x|\mu,\sigma^2)
=
\frac{1}{\sqrt{2\pi\sigma^2}}
e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

There are two parameters:

* \(\mu\) = mean
* \(\sigma^2\) = variance

We observe some data and want to estimate these parameters.

---

# 2. Our Goal

Suppose we observe:

```text id="l1c9b3"
10, 12, 15, 18, 20
```

We assume:

$$
X_1,X_2,\ldots,X_n
\sim N(\mu,\sigma^2)
$$

But we don't know:

$$
\mu
$$

or:

$$
\sigma^2
$$

We want to find:

$$
\hat{\mu}
$$

and:

$$
\hat{\sigma}^2
$$

using Maximum Likelihood.

---

# 3. What Does MLE Ask?

Remember the MLE idea:

> **Find the parameter values that make the observed data most plausible.**

So we're asking:

```text id="r0l8cz"
Observed data
      ↓
Try different μ and σ²
      ↓
How well do they explain the data?
      ↓
Find the values producing
maximum likelihood
```

---

# 4. Write the Likelihood

For one observation:

$$
f(x_i|\mu,\sigma^2)
=
\frac{1}{\sqrt{2\pi\sigma^2}}
e^{-\frac{(x_i-\mu)^2}{2\sigma^2}}
$$

If the observations are independent, the likelihood of all \(n\) observations is the product:

$$
L(\mu,\sigma^2)
=
\prod_{i=1}^{n}
f(x_i|\mu,\sigma^2)
$$

Substitute the Normal PDF:

$$
L(\mu,\sigma^2)
=
\prod_{i=1}^{n}
\frac{1}{\sqrt{2\pi\sigma^2}}
e^{-\frac{(x_i-\mu)^2}{2\sigma^2}}
$$

---

# 5. Simplify the Likelihood

There are \(n\) identical normalization terms:

$$
\frac{1}{\sqrt{2\pi\sigma^2}}
$$

So:

$$
L(\mu,\sigma^2)
=
\left(
\frac{1}{\sqrt{2\pi\sigma^2}}
\right)^n
\prod_{i=1}^{n}
e^{-\frac{(x_i-\mu)^2}{2\sigma^2}}
$$

Using:

$$
\prod_i e^{a_i}=e^{\sum_i a_i}
$$

we get:

$$
L(\mu,\sigma^2)
=
(2\pi\sigma^2)^{-n/2}
e^{-\frac{1}{2\sigma^2}
\sum_{i=1}^{n}(x_i-\mu)^2}
$$

So:

$$
\boxed{
L(\mu,\sigma^2)
=
(2\pi\sigma^2)^{-n/2}
e^{-\frac{\sum(x_i-\mu)^2}{2\sigma^2}}
}
$$

---

# 6. Why Take the Log?

The likelihood contains products and exponentials.

So, just like with the Binomial and Exponential distributions, we take the logarithm.

$$
\ell(\mu,\sigma^2)
=
\log L(\mu,\sigma^2)
$$

Using log rules:

$$
\boxed{
\ell(\mu,\sigma^2)
=
-\frac n2\log(2\pi)
-\frac n2\log(\sigma^2)
-\frac{1}{2\sigma^2}
\sum_{i=1}^{n}(x_i-\mu)^2
}
$$

Now the problem is much easier to differentiate.

---

# 7. First Estimate \(\mu\)

We have two unknown parameters:

$$
\mu,\sigma^2
$$

Let's first find the MLE for \(\mu\).

Take the derivative of the log-likelihood with respect to \(\mu\):

$$
\frac{\partial\ell}{\partial\mu}
$$

The only term involving \(\mu\) is:

$$
-\frac{1}{2\sigma^2}
\sum_{i=1}^{n}(x_i-\mu)^2
$$

Differentiate:

$$
\frac{\partial\ell}{\partial\mu}
=
\frac{1}{\sigma^2}
\sum_{i=1}^{n}(x_i-\mu)
$$

Set it equal to zero:

$$
\frac{1}{\sigma^2}
\sum_{i=1}^{n}(x_i-\mu)
=
0
$$

Since \(\sigma^2>0\):

$$
\sum_{i=1}^{n}(x_i-\mu)=0
$$

Expand:

$$
\sum x_i-n\mu=0
$$

Therefore:

$$
n\mu=\sum x_i
$$

and:

$$
\boxed{
\hat\mu=\frac{\sum x_i}{n}
}
$$

But that's exactly the sample mean:

$$
\boxed{\hat\mu=\bar{x}}
$$

---

# 8. Why Does the MLE of \(\mu\) Equal the Mean?

This result makes intuitive sense.

The Normal distribution is centered at:

$$
\mu
$$

So if we want the Normal distribution to best fit our observed data, its center should be at the center of the data.

The sample mean is that center.

```text id="r8e2qp"
Observed data

     • • • • •
───────────────
       ↑
     mean

       ↓

Best Normal center

       μ̂ = x̄
```

So:

> **MLE puts the Normal distribution's center at the sample mean.**

---

# 9. Now Estimate \(\sigma^2\)

Now we want the MLE for variance.

Start again with:

$$
\ell(\mu,\sigma^2)
=
-\frac n2\log(2\pi)
-\frac n2\log(\sigma^2)
-\frac{1}{2\sigma^2}
\sum(x_i-\mu)^2
$$

It's convenient to treat:

$$
v=\sigma^2
$$

as the parameter.

Then:

$$
\ell(\mu,v)
=
-\frac n2\log(2\pi)
-\frac n2\log v
-\frac{1}{2v}
\sum(x_i-\mu)^2
$$

---

# 10. Differentiate With Respect to Variance

Take:

$$
\frac{\partial\ell}{\partial v}
$$

We get:

$$
-\frac{n}{2v}
+
\frac{1}{2v^2}
\sum(x_i-\mu)^2
$$

Set equal to zero:

$$
-\frac{n}{2v}
+
\frac{1}{2v^2}
\sum(x_i-\mu)^2
=
0
$$

Multiply by \(2v^2\):

$$
-nv+\sum(x_i-\mu)^2=0
$$

Therefore:

$$
nv=\sum(x_i-\mu)^2
$$

So:

$$
v=
\frac{1}{n}
\sum(x_i-\mu)^2
$$

Replace \(v\) with \(\sigma^2\):

$$
\boxed{
\hat{\sigma}^2
=
\frac{1}{n}
\sum_{i=1}^{n}(x_i-\mu)^2
}
$$

But we don't know the true \(\mu\).

The MLE estimate of \(\mu\) is:

$$
\hat\mu=\bar{x}
$$

Therefore:

$$
\boxed{
\hat{\sigma}^2_{MLE}
=
\frac{1}{n}
\sum_{i=1}^{n}(x_i-\bar{x})^2
}
$$

---

# 11. The Final MLE Results

For:

$$
X_1,\ldots,X_n\sim N(\mu,\sigma^2)
$$

the maximum likelihood estimates are:

$$
\boxed{\hat{\mu}_{MLE}=\bar{x}}
$$

and:

$$
\boxed{
\hat{\sigma}^2_{MLE}
=
\frac{1}{n}
\sum_{i=1}^{n}(x_i-\bar{x})^2
}
$$

These are among the most important MLE results in statistics.

---

# 12. Wait... Why \(n\), Not \(n-1\)?

This connects directly to our earlier discussion.

The familiar sample variance is:

$$
s^2=
\frac{1}{n-1}
\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

But MLE gives:

$$
\hat{\sigma}^2_{MLE}
=
\frac{1}{n}
\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

Why?

Because these are answering **different questions**.

### MLE

Find the parameter that maximizes the likelihood.

### Unbiased estimation

Find an estimator whose expected value equals the true parameter.

These goals do not always produce the same estimator.

---

# 13. The Bias of the MLE Variance

It can be shown that:

$$
E\left[
\frac1n
\sum_{i=1}^{n}(X_i-\bar X)^2
\right]
=
\frac{n-1}{n}\sigma^2
$$

Therefore:

$$
E[\hat{\sigma}^2_{MLE}]
=
\frac{n-1}{n}\sigma^2
$$

So the MLE variance estimator is slightly biased downward.

The unbiased estimator uses:

$$
n-1
$$

instead.

```text id="83du7f"
MLE variance:

Σ(xᵢ − x̄)²
─────────────
      n


Unbiased sample variance:

Σ(xᵢ − x̄)²
─────────────
     n − 1
```

---

# 14. Why Is the MLE Variance Too Small?

Remember:

$$
\bar{x}
$$

was calculated from the same data.

The sample mean is chosen specifically to minimize:

$$
\sum(x_i-a)^2
$$

over \(a\).

So:

$$
\sum(x_i-\bar{x})^2
$$

is systematically smaller than it would be if we knew and used the true population mean \(\mu\).

That is why dividing by \(n\) tends to underestimate the population variance.

---

# 15. A Numerical Example

Suppose:

```text id="a0qv2m"
Data:

10, 20, 30
```

The mean is:

$$
\bar{x}=20
$$

Calculate squared deviations:

$$
(10-20)^2=100
$$

$$
(20-20)^2=0
$$

$$
(30-20)^2=100
$$

Sum:

$$
100+0+100=200
$$

### MLE variance

$$
\hat{\sigma}^2_{MLE}
=
\frac{200}{3}
$$

$$
\boxed{66.67}
$$

### Unbiased sample variance

$$
s^2=
\frac{200}{2}
$$

$$
\boxed{100}
$$

Same data.

Different objectives.

---

# 16. Why Does MLE Choose This Variance?

Think about the Normal distribution.

If:

$$
\sigma^2
$$

is too small:

```text id="k3u9xm"
       Narrow distribution
            /\
           /  \
          /    \
─────────/──────\─────────
```

The distribution doesn't cover the observed data well.

If:

$$
\sigma^2
$$

is too large:

```text id="z7gc7b"
       Wide distribution
      ____________
     /            \
────/──────────────\────
```

The distribution becomes unnecessarily spread out.

MLE finds the value that provides the best overall fit to the observed observations.

---

# 17. What Does "Best Fit" Mean?

It means:

> **The Normal distribution with these parameter values gives the largest likelihood to the observed data.**

So MLE is not simply:

> "Draw the curve that looks nicest."

It is a mathematically defined optimization problem.

```text id="xq9czo"
Data
 ↓
Normal model
 ↓
Try μ and σ²
 ↓
Calculate likelihood
 ↓
Find maximum
 ↓
μ̂ = x̄
σ̂² = Σ(xᵢ-x̄)²/n
```

---

# 18. Why the Mean and Variance Appear Together

The Normal distribution has two jobs:

### \(\mu\)

Controls **where the distribution is centered**.

### \(\sigma^2\)

Controls **how spread out it is**.

Therefore MLE asks:

```text id="x9q9ac"
Where should the Normal curve be centered?
             ↓
          μ̂ = x̄


How wide should it be?
             ↓
σ̂² = average squared deviation
```

This makes the result very intuitive.

---

# 19. Another Beautiful Connection: Least Squares

Remember linear regression.

OLS minimizes:

$$
\sum(y_i-\hat y_i)^2
$$

Now look at the Normal likelihood.

The log-likelihood contains:

$$
-\frac{1}{2\sigma^2}
\sum(x_i-\mu)^2
$$

Maximizing it with respect to \(\mu\) is equivalent to minimizing:

$$
\sum(x_i-\mu)^2
$$

And the value that minimizes squared deviations is:

$$
\boxed{\mu=\bar{x}}
$$

So:

```text id="8e8q81"
Normal likelihood
       ↓
Squared deviations
       ↓
Minimize squared errors
       ↓
Mean
```

This is one reason the mean is so important in Normal-based statistics.

---

# 20. MLE and Linear Regression

This connection becomes even more powerful.

Suppose:

$$
Y_i=\beta_0+\beta_1X_i+\epsilon_i
$$

and:

$$
\epsilon_i\sim N(0,\sigma^2)
$$

Then the likelihood of the data depends on:

$$
\sum_i(y_i-\hat y_i)^2
$$

Maximizing the likelihood with respect to the regression coefficients is equivalent to minimizing:

$$
\boxed{
\sum_i(y_i-\hat y_i)^2
}
$$

That's exactly **ordinary least squares**.

So:

> **OLS can be derived as Maximum Likelihood under normally distributed errors.**

---

# 21. MLE and the Normal Distribution: Big Connection

We've now connected:

```text id="l4wj56"
Normal distribution
        ↓
Likelihood
        ↓
Log-likelihood
        ↓
Squared deviations
        ↓
Maximum likelihood
        ↓
Mean + variance
        ↓
Least squares
        ↓
Linear regression
```

This is one of the most useful conceptual connections in statistics.

---

# 22. Why the Log-Likelihood Is So Useful

The original likelihood is:

$$
L(\mu,\sigma^2)
=
(2\pi\sigma^2)^{-n/2}
e^{-\frac{\sum(x_i-\mu)^2}{2\sigma^2}}
$$

It can become extremely small as \(n\) increases.

The log-likelihood:

$$
\ell(\mu,\sigma^2)
=
-\frac n2\log(2\pi)
-\frac n2\log(\sigma^2)
-\frac{\sum(x_i-\mu)^2}{2\sigma^2}
$$

is much easier to work with.

And because logarithm is monotonic:

$$
\boxed{
\arg\max L
=
\arg\max\log L
}
$$

So we haven't changed the MLE.

We've just made the mathematics easier.

---

# 23. What If \(\sigma\) Is the Parameter Instead?

Sometimes the Normal distribution is written using:

$$
\sigma
$$

instead of:

$$
\sigma^2
$$

The PDF is:

$$
f(x|\mu,\sigma)
=
\frac{1}{\sqrt{2\pi}\sigma}
e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

The MLE for standard deviation is then:

$$
\boxed{
\hat\sigma_{MLE}
=
\sqrt{
\frac1n
\sum_{i=1}^{n}(x_i-\bar{x})^2
}
}
$$

Notice again:

$$
\text{MLE SD}
=
\sqrt{\text{MLE variance}}
$$

---

# 24. A Subtle Point About Variance

It's tempting to say:

> "The MLE variance is wrong because it uses \(n\)."

That's not correct.

It's simply optimizing a **different criterion**.

The MLE:

$$
\frac1n\sum(x_i-\bar{x})^2
$$

is biased for finite samples but has other desirable properties, including consistency under the standard Normal model.

The \(n-1\) estimator is unbiased.

So:

```text id="n0yp9e"
MLE ≠ unbiasedness

They are different properties.
```

---

# 25. Common Mistakes

### ❌ "MLE always gives the unbiased estimator."

No.

The Normal variance MLE is a classic counterexample.

---

### ❌ "The MLE variance should use \(n-1\)."

Not if you're specifically deriving the MLE.

The MLE uses:

$$
\boxed{n}
$$

---

### ❌ "MLE and least squares are unrelated."

No.

Under Gaussian errors, maximizing likelihood gives least squares.

---

### ❌ "The Normal distribution requires the sample mean and sample variance."

The Normal **model** has population parameters \(\mu\) and \(\sigma^2\).

The MLEs estimate them from data.

---

### ❌ "MLE proves the data are Normal."

No.

You must choose the Normal model and then estimate its parameters. Model adequacy is a separate question.

---

# 26. The Entire Derivation in One View

```text id="f5zv2k"
Assume:

X₁,...,Xₙ ~ Normal(μ, σ²)

          ↓

Write likelihood:

L(μ,σ²)
= ∏ f(xᵢ|μ,σ²)

          ↓

Take log:

ℓ(μ,σ²)

          ↓

Differentiate with respect to μ:

∂ℓ/∂μ = 0

          ↓

μ̂ = x̄

          ↓

Differentiate with respect to σ²:

∂ℓ/∂σ² = 0

          ↓

σ̂² = Σ(xᵢ − x̄)² / n
```

---

# 27. Final Results to Memorize

For:

$$
X_1,\ldots,X_n\sim N(\mu,\sigma^2)
$$

the MLEs are:

$$
\boxed{\hat{\mu}_{MLE}=\bar{x}}
$$

and:

$$
\boxed{
\hat{\sigma}^2_{MLE}
=
\frac{1}{n}
\sum_{i=1}^{n}(x_i-\bar{x})^2
}
$$

Therefore:

$$
\boxed{
\hat{\sigma}_{MLE}
=
\sqrt{
\frac{1}{n}
\sum_{i=1}^{n}(x_i-\bar{x})^2
}
}
$$

---

# 🧠 Mental Model

Think of fitting a Normal curve to your data.

You have two knobs:

```text
        Normal distribution

             μ
             ↓
        Where is the
        curve centered?

             σ²
             ↓
        How wide is
        the curve?
```

MLE turns the knobs until the observed data are **most likely**.

The result is:

```text
Center
  ↓
μ̂ = x̄

Spread
  ↓
σ̂² = average squared deviation from x̄
```

And remember the subtle point:

> **MLE variance divides by \(n\); unbiased sample variance divides by \(n-1\).**

---

## 🎯 Interview-Ready Answer

> For independent observations assumed to come from $N(\mu,\sigma^2)$, we write the joint likelihood, take its logarithm, and maximize it with respect to $\mu$ and $\sigma^2$. Differentiating with respect to $\mu$ gives
>
> $$
> \hat{\mu} = \bar{x}
> $$
>
> Differentiating with respect to $\sigma^2$ then gives
>
> $$
> \hat{\sigma}^2 = \frac{1}{n}\sum (x_i-\bar{x})^2
> $$
>
> Thus, the Normal MLE estimates the mean using the **sample mean** and the variance using the **average squared deviation from that mean**. The variance MLE divides by $n$, not $(n-1)$, because **MLE and unbiased estimation are different objectives**.

---

## 🔑 One-Line Takeaway

> For a Normal distribution, **Maximum Likelihood puts the mean at the sample mean and the variance at the average squared deviation from that mean**:
>
> $$
> \boxed{
> \hat{\mu}=\bar{x},\qquad
> \hat{\sigma}^2=\frac{1}{n}\sum (x_i-\bar{x})^2
> }
> $$
